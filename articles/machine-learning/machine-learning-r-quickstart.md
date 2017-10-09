---
title: "Samouczek aaaQuickstart dla języka R Machine Learning | Dokumentacja firmy Microsoft"
description: "Użyj tego R programowania samouczek tooget uruchomiona szybko przy użyciu języka hello R w usłudze Azure Machine Learning Studio toocreate prognozowania rozwiązania."
keywords: "Szybki Start, języka r, r język programowania, samouczek programowania r"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 99a3a0fd-b359-481a-b236-66868deccd96
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: garye
ms.openlocfilehash: 9995f8728f4d7bf9a5c15412015e4cf769cdac96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-tutorial-for-hello-r-programming-language-for-azure-machine-learning"></a>Samouczek szybki start dotyczący hello R język programowania dla usługi Azure Machine Learning

<!-- Stephen F Elston, Ph.D. -->

## <a name="introduction"></a>Wprowadzenie
Ten samouczek Szybki Start pomaga szybko rozpocząć rozszerzanie uczenia maszynowego Azure przy użyciu języka programowania hello R. Postępuj zgodnie z tym R programowania toocreate samouczek, przetestować i wykonanie kodu języka R w usłudze Azure Machine Learning. Podczas pracy z samouczkiem utworzysz kompletnego rozwiązania prognozowania przy użyciu języka hello R w usłudze Azure Machine Learning.  

Microsoft Azure Machine Learning zawiera wiele modułów wydajny komputer uczenie i danych manipulowanie. Hello zaawansowanych język R został opisany jako franca język hello analizy. Happily manipulowanie analizy i danych w usłudze Azure Machine Learning można rozszerzyć za pomocą R. Ta kombinacja zapewnia hello skalowalność i łatwość wdrażania usługi Azure Machine Learning hello elastyczność i analiza głębokie r.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

### <a name="forecasting-and-hello-dataset"></a>Prognozowanie i hello zestawu danych
Funkcja prognozowania jest powszechnie pracowników i bardzo przydatne metody analitycznej. Wspólne używa zakresu z przewidywania sprzedaży elementów okresach Określanie optymalnego zapasów, zmienne makroekonomicznej toopredicting. Funkcja prognozowania jest zazwyczaj wykonywane z modeli szeregów czasowych.

Czas serii danych jest danych, w którym wartości hello ma indeks czasu. Indeks czasu Hello może być regularnie, np. co miesiąc lub co minutę lub nieprawidłowo. Model szeregów czasowych jest na podstawie czasu serii danych. język programowania Hello R zawiera elastyczną architekturę i szeroką gamę analiza czasu serii danych.

W tym przewodniku Szybki Start możemy zostanie praca z mleczarskie Kalifornijskiej i cenach danych. Te dane obejmują informacje miesięczne na powitania produkcji kilka mleczarskich i hello ceny mleka fat zwykłych stawek.

dane Hello używane w tym artykule, wraz ze skryptami R, mogą być [pobrana w tym miejscu][download]. Te dane został pierwotnie syntezatora z informacji dostępnych w hello uniwersytecie Wisconsin na http://future.aae.wisc.edu/tab/production.html.

### <a name="organization"></a>Organizacja
Firma Microsoft będzie postęp kilku kroków jako dowiesz się, jak toocreate, testowanie i wykonanie kodu manipulowania R analizy i danych w środowisku Azure Machine Learning hello.  

* Najpierw przeanalizujemy podstawy hello przy użyciu języka hello R w środowisku Azure Machine Learning Studio hello.
* Następnie możemy postępu toodiscussing różnych aspektów we/wy dla danych, kodu języka R i grafiki w środowisku Azure Machine Learning hello.
* Firma Microsoft będzie skonstruować hello pierwsza część naszego prognozowania rozwiązania przez utworzenie kodu do czyszczenia danych i przekształcania.
* Z naszych danych przygotowane zostaną wykonane analizę hello korelacji między kilka hello zmiennych w naszym zestawie danych.
* Na koniec utworzymy model prognozowania szeregów czasowych okresach do produkcji mleka.

## <a id="mlstudio"></a>Interakcje z języka R w usłudze Machine Learning Studio
W tej sekcji przedstawia niektóre podstawowe informacje o interakcji z języka programowania hello R w środowisku usługi Machine Learning Studio hello. język Hello R udostępnia zaawansowane narzędzia toocreate dostosowane analizy i danych manipulowania modułów w środowisku Azure Machine Learning hello.

Użyję programu RStudio toodevelop, badanie i debugowania kodu R na małą skalę. Ten kod jest następnie wycinanie i wklejanie w [wykonanie skryptu języka R] [ execute-r-script] modułu w toorun gotowy Machine Learning Studio.  

### <a name="hello-execute-r-script-module"></a>Witaj modułu wykonania skryptu języka R
W usłudze Machine Learning Studio, R skrypty są uruchamiane w ramach hello [wykonanie skryptu języka R] [ execute-r-script] modułu. Przykład Witaj [wykonanie skryptu języka R] [ execute-r-script] modułu w usłudze Machine Learning Studio jest pokazany na rysunku 1.

 ![R język programowania: hello modułu wykonania skryptu języka R wybrane w usłudze Machine Learning Studio][1]

*Rysunek 1. środowiska usługi Machine Learning Studio Hello przedstawiający modułu wykonania skryptu języka R hello wybrane.*

Odwoływanie tooFigure 1, Przyjrzyjmy się niektóre z kluczowych części środowiska usługi Machine Learning Studio hello do pracy z hello hello [wykonanie skryptu języka R] [ execute-r-script] modułu.

* Moduły Hello w eksperymencie hello są wyświetlane w okienku Centrum hello.
* Witaj górna część hello w prawym okienku zawiera tooview okna i edycji skryptów R.  
* Witaj dolnej części prawym okienku przedstawia niektóre właściwości hello [wykonanie skryptu języka R][execute-r-script]. Dzienniki błędów i dane wyjściowe hello można wyświetlić, klikając odpowiednie punkty hello tego okienka.

Firma Microsoft będzie oczywiście w niniejszym dokumencie hello [wykonanie skryptu języka R] [ execute-r-script] bardziej szczegółowo na powitania pozostałej części tego dokumentu.

Podczas pracy z złożonych funkcji R, zalecamy edytować, testowania i debugowania w programu RStudio. Podobnie jak w przypadku dowolnego rozwoju oprogramowania przyrostowo rozszerzyć kodu i przetestować go na małych prostych przypadkach testowych. Następnie wycinanie i wklejanie funkcji do okna skryptu hello R hello [wykonanie skryptu języka R] [ execute-r-script] modułu. Takie podejście umożliwia tooharness zarówno hello programu RStudio zintegrowane środowisko programistyczne (IDE) i hello możliwości usługi Azure Machine Learning.  

#### <a name="execute-r-code"></a>Wykonanie kodu języka R
Kod języka R w hello [wykonanie skryptu języka R] [ execute-r-script] modułu zostanie wykonany po uruchomieniu hello eksperyment, klikając hello **Uruchom** przycisku. Po zakończeniu wykonywania znacznik wyboru pojawią się na powitania [wykonanie skryptu języka R] [ execute-r-script] ikony.

#### <a name="defensive-r-coding-for-azure-machine-learning"></a>Kodowanie obrony R dla usługi Azure Machine Learning
Jeśli tworzysz kodu R, na przykład usługi sieci web przy użyciu usługi Azure Machine Learning, należy ostatecznie zaplanować, jak kod zajmuje się nieoczekiwane dane wejściowe i wyjątki. toomaintain przejrzystości, I nie zostały uwzględnione sposób hello sprawdzanie lub obsługi wyjątków w większości podane przykłady kodu hello. Jednak jak możemy kontynuować I zapewni kilka przykładów funkcji przy użyciu możliwości obsługi wyjątków, R.  

Jeśli potrzebujesz bardziej szczegółowy traktowanie Obsługa wyjątków języka R, najlepiej odczytu hello odpowiednie części podręcznika hello przez Wickham wymienionych w [dodatek B — dalsze informacje](#appendixb).

#### <a name="debug-and-test-r-in-machine-learning-studio"></a>Debugowania i testowania R w usłudze Machine Learning Studio
tooreiterate, I zaleca się testowanie i debugowanie kodu języka R na małą skalę w programu RStudio. Istnieją jednak przypadki, w których konieczne tootrack dół problemów kodu języka R w hello [wykonanie skryptu języka R] [ execute-r-script] samej siebie. Ponadto jest dobrym rozwiązaniem toocheck wyniki w usłudze Machine Learning Studio.

Dane wyjściowe wykonania hello kodu języka R i na platformie Azure Machine Learning hello znajduje się głównie w dane_wyjściowe.log. Dodatkowe informacje będą widoczne w error.log.  

Jeśli w usłudze Machine Learning Studio występuje błąd podczas uruchamiania kodu języka R, pierwszy przebiegu działań powinny być toolook na error.log. Ten plik może zawierać błąd przydatne wiadomości toohelp zrozumieć i poprawić ten błąd. error.log tooview, kliknij przycisk **dziennik błędów w widoku** na powitania **w okienku właściwości** dla hello [wykonanie skryptu języka R] [ execute-r-script] zawierające błąd hello.

Na przykład został uruchomiony hello następującego kodu R, niezdefiniowane y zmiennej w [wykonanie skryptu języka R] [ execute-r-script] modułu:

    x <- 1.0
    z <- x + y

Ten kod nie powiedzie się tooexecute, co powoduje wystąpienie stanu błędu. Kliknięcie **dziennik błędów w widoku** na powitania **w okienku właściwości** tworzy hello wyświetlania pokazany na rysunku 2.

  ![Komunikat o błędzie wyskakującego okienka][2]

*Rysunek 2. Komunikat o błędzie wyskakujących.*

Wygląda na to, potrzebujemy toolook w komunikacie o błędzie dane_wyjściowe.log toosee hello R. Polecenie hello [wykonanie skryptu języka R] [ execute-r-script] , a następnie kliknij polecenie hello **wyświetlić dane_wyjściowe.log** element na powitania **w okienku właściwości** toohello prawo. Otwiera nowe okno przeglądarki i są widoczne następujące hello.

    [Critical]     Error: Error 0063: hello following error occurred during evaluation of R script:
    ---------- Start of error message from R ----------
    object 'y' not found


    object 'y' not found
    ----------- End of error message from R -----------

Ten komunikat o błędzie zawiera nie niespodzianki i jasno identyfikuje hello problem.

wartość hello tooinspect wszystkich obiektów w R, możesz wydrukować pliku dane_wyjściowe.log toohello tych wartości. reguły Hello badania obiektu wartości są zasadniczo hello takie same jak w sesji interaktywnej R. Na przykład jeśli wpiszesz nazwę zmiennej w wierszu, wartość hello hello obiektu będzie drukowanej toohello dane_wyjściowe.log pliku.  

#### <a name="packages-in-machine-learning-studio"></a>Pakiety w usłudze Machine Learning Studio
Usługa Azure Machine Learning jest dostarczany z ponad 350 wstępnie zainstalowane pakiety języka R. Można użyć następującego kodu w hello hello [wykonanie skryptu języka R] [ execute-r-script] tooretrieve modułu listę hello wstępnie zainstalowane pakiety.

    data.set <- data.frame(installed.packages())
    maml.mapOutputPort("data.set")

Jeśli nie znasz hello ostatniego wiersza kodu w chwili hello, poniżej. W hello pozostałej części tego dokumentu często omówimy użycia języka R w środowisku Azure Machine Learning hello.

### <a name="introduction-toorstudio"></a>Wprowadzenie tooRStudio
Programu RStudio jest powszechnie używaną IDE dla R. Użyję programu RStudio edycji, testowanie i debugowanie części kodu hello R używanych w tym przewodniku Szybki start. Po kodzie R przetestowane i gotowe, po prostu wyciąć i wkleić w edytorze programu RStudio hello w usłudze Machine Learning Studio [wykonanie skryptu języka R] [ execute-r-script] modułu.  

Jeśli nie masz hello R język programowania zainstalowana na tym komputerze pulpitu, zaleca się, że możesz to zrobić teraz. Bezpłatne materiały do pobrania języka typu open source R są dostępne pod adresem hello kompleksowe R sieci (CRAN archiwum sieci) w [http://www.r-project.org/](http://www.r-project.org/). Brak dostępnych pliki do pobrania dla systemu Windows, Mac OS i Linux/UNIX. Wybierz pobliskich dublowania i postępuj zgodnie z instrukcjami pobierania hello. Ponadto sieci CRAN zawiera wiele pakietów manipulowania przydatne analizy i danych.

W przypadku nowych tooRStudio należy pobrać i zainstalować wersję pulpitu hello. Można znaleźć powitalne programu RStudio w http://www.rstudio.com/products/RStudio/ pobiera systemu Windows, Mac OS i Linux/UNIX. Postępuj zgodnie z instrukcjami hello podane tooinstall programu RStudio na komputerze pulpitu.  

TooRStudio samouczka Wprowadzenie jest dostępny na https://support.rstudio.com/hc/sections/200107586-Using-RStudio.

I Podaj dodatkowe informacje na temat używania programu RStudio w [dodatek a.][appendixa].  

## <a id="scriptmodule"></a>Pobieranie danych i modułu wykonania skryptu języka R hello
W tej sekcji omówimy, jak pobrać dane do i z hello [wykonanie skryptu języka R] [ execute-r-script] modułu. Zapoznamy się, jak toohandle różne typy danych do odczytu do i z hello [wykonanie skryptu języka R] [ execute-r-script] modułu.

Hello kompletny kod dla tej sekcji znajduje się w pliku zip hello pobrany wcześniej.

### <a name="load-and-check-data-in-machine-learning-studio"></a>Załadowanie i sprawdzenie, czy dane w usłudze Machine Learning Studio
#### <a id="loading"></a>Zestaw danych hello obciążenia
Rozpoczniemy ładując hello **csdairydata.csv** pliku do usługi Azure Machine Learning Studio.

* Uruchom środowiska Azure Machine Learning Studio.
* Polecenie **+ nowy** na powitania lewy ekranu i wybierz dolny **zestawu danych**.
* Wybierz **z pliku lokalnego**, a następnie **Przeglądaj** tooselect hello pliku.
* Upewnij się, że wybrano **pliku CSV ogólnego z nagłówkiem (.csv)** jako typ hello hello zestawu danych.
* Kliknij znacznik wyboru hello.
* Po przekazaniu hello zestawu danych, powinny pojawić się hello nowy zestaw danych, klikając hello **zestawów danych** kartę.  

#### <a name="create-an-experiment"></a>Tworzenie eksperymentu
Teraz, gdy mamy niektóre dane w usłudze Machine Learning Studio, potrzebujemy toocreate analizę hello toodo eksperymentu.  

* Polecenie **+ nowy** na powitania lewy dolny i wybierz **eksperymentu**, następnie **pusty eksperyment**.
* Nazwa eksperymentu, wybierając i modyfikowanie hello **eksperymentu utworzony na...**  tytuł u góry hello hello strony. Na przykład zmiana zbyt**urzędu certyfikacji Nabiał analizy**.
* Na powitania po lewej stronie eksperymentu hello, rozwiń **zapisane zestawów danych**, a następnie **Moje zestawów danych**. Powinny pojawić się hello **cadairydata.csv** który został wcześniej przekazany.
* Przeciąganie i upuszczanie hello **csdairydata.csv dataset** na powitania eksperymentu.
* W hello **wyszukiwania eksperymentu elementów** pole na powitania górnej części okienka po lewej stronie powitania, typu [wykonanie skryptu języka R][execute-r-script]. Zostanie wyświetlone modułu hello są wyświetlane na liście wyszukiwania hello.
* Przeciąganie i upuszczanie hello [wykonanie skryptu języka R] [ execute-r-script] modułu na Twoje palety.  
* Połącz dane wyjściowe hello hello **csdairydata.csv dataset** toohello po lewej stronie dane wejściowe (**Dataset1**) z hello [wykonanie skryptu języka R][execute-r-script].
* **Nie zapomnij tooclick "Zapisz"!**  

W tym momencie eksperymentu powinien wyglądać jak rysunek 3.

![Witaj analizy Nabiał urzędu certyfikacji eksperymentów z zestawu danych i modułu wykonania skryptu języka R][3]

*Rysunek 3. Witaj analizy Nabiał urzędu certyfikacji Eksperymentuj z zestawu danych i modułu wykonania skryptu języka R.*

#### <a name="check-on-hello-data"></a>Sprawdź na powitania danych
Załóżmy mają wygląd hello dane, które firma Microsoft zostały załadowane na naszym doświadczeniu. W eksperymencie powitania kliknij hello dane wyjściowe hello **cadairydata.csv dataset** i wybierz **wizualizacji**. Powinny zostać wyświetlone informacje takie jak rysunek 4.  

![Podsumowanie hello cadairydata.csv w zestawie danych][4]

*Rysunek 4. Podsumowanie hello cadairydata.csv dataset.*

W tym widoku widzimy wiele przydatnych informacji. Zobaczysz hello pierwsze kilka wierszy tego zestawu danych. Zaznaczenie kolumny, hello sekcji Statystyki zawiera więcej informacji na temat hello kolumny. Na przykład hello typu funkcji wiersza pokazuje nam, jakie typy danych Azure Machine Learning Studio przypisane toohello kolumny. Krótki przegląd podobny do tego jest wyboru związane z poprawnością dobra przed Rozpoczniemy toodo poważne pracę.

### <a name="first-r-script"></a>Pierwszy skrypt języka R
W usłudze Azure Machine Learning Studio Utwórz prosty pierwszy R skryptu tooexperiment z. Po utworzeniu i przetestowane hello następującego skryptu programu RStudio.  

    ## Only one of hello following two lines should be used
    ## If running in Machine Learning Studio, use hello first line with maml.mapInputPort()
    ## If in RStudio, use hello second line with read.csv()
    cadairydata <- maml.mapInputPort(1)
    # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
    str(cadairydata)
    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata)
    ## hello following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('cadairydata')

Teraz potrzebuję tootransfer tooAzure tego skryptu Machine Learning Studio. I może po prostu wyciąć i wkleić. Jednak w takim przypadku I przenieś Moje skrypt języka R za pomocą pliku zip.

### <a name="data-input-toohello-execute-r-script-module"></a>Moduł wykonanie skryptu języka R toohello wprowadzania danych
Załóżmy ma przyjrzeć się toohello dane wejściowe hello [wykonanie skryptu języka R] [ execute-r-script] modułu. W tym przykładzie firma Microsoft będzie odczytywać dane mleczarskich Kalifornijskiej hello na powitania [wykonanie skryptu języka R] [ execute-r-script] modułu.  

Istnieją trzy możliwe dane wejściowe dla hello [wykonanie skryptu języka R] [ execute-r-script] modułu. W zależności od aplikacji, można użyć dowolnego lub wszystkich tych danych wejściowych. Możliwe jest również doskonale uzasadnione toouse R skrypt, który nie wymaga danych wejściowych w ogóle.  

Przyjrzyjmy się każdy z tych danych wejściowych z tooright po lewej stronie. Widać nazwy hello każdego wejścia hello umieszczając kursor nad hello danych wejściowych i odczytywania hello etykietka narzędzia.  

#### <a name="script-bundle"></a>Skrypt pakietu
Witaj danych wejściowych skryptu pakietu pozwala toopass hello zawartość pliku zip do [wykonanie skryptu języka R] [ execute-r-script] modułu. Można użyć jednego hello następujące polecenia tooread hello zawartość pliku zip hello w kodzie języka R.

    source("src/yourfile.R") # Reads a zipped R script
    load("src/yourData.rdata") # Reads a zipped R data file

> [!NOTE]
> Usługa Azure Machine Learning traktuje plików hello zip tak, jakby znajdują się w hello src / directory, w związku z czym należy tooprefix nazwy pliku o tej nazwie w katalogu. Na przykład jeśli hello zip zawiera pliki hello `yourfile.R` i `yourData.rdata` w głównym hello hello zip, czy adres je jako `src/yourfile.R` i `src/yourData.rdata` przy użyciu `source` i `load`.
> 
> 

Omówiono już zestawy danych ładowania [podczas ładowania zestawu danych hello](#loading). Po utworzeniu i przetestować skrypt hello R wyświetlone w poprzedniej sekcji hello hello następujące:

1. Zapisz skrypt hello R do. Plik R. Można wywołać pliku skryptu "simpleplot. R". Oto hello zawartość.
   
        ## Only one of hello following two lines should be used
        ## If running in Machine Learning Studio, use hello first line with maml.mapInputPort()
        ## If in RStudio, use hello second line with read.csv()
        cadairydata <- maml.mapInputPort(1)
        # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
        str(cadairydata)
        pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata)
        ## hello following line should be executed only when running in
        ## Azure Machine Learning Studio
        maml.mapOutputPort('cadairydata')
2. Utwórz plik zip i skopiuj skrypt do tego pliku zip. W systemie Windows, kliknij prawym przyciskiem myszy na powitania plik i wybierz **przesyłają**, a następnie **skompresowanego folderu**. Spowoduje to utworzenie nowego pliku zip zawierającego powitania "simpleplot. Plik R".
3. Dodaj z pliku toohello **zestawów danych** w usłudze Machine Learning Studio, określając hello typ jako **zip**. Plik zip hello powinna zostać wyświetlona w zestawów danych.
4. Przeciąganie i upuszczanie plików zip hello z **zestawów danych** na powitania **kanwy ML Studio**.
5. Połącz dane wyjściowe hello hello **zip danych** toohello ikona **pakietu skryptu** wejściowych z hello [wykonanie skryptu języka R] [ execute-r-script] modułu.
6. Typ hello `source()` funkcji z nazwy pliku zip do okna Kod powitania dla hello [wykonanie skryptu języka R] [ execute-r-script] modułu. W przypadku mojej wpisane `source("src/simpleplot.R")`.  
7. Upewnij się, że możesz kliknąć pozycję **zapisać**.

Po zakończeniu tych czynności hello [wykonanie skryptu języka R] [ execute-r-script] modułu wykona hello R skryptu w pliku zip powitania po uruchomieniu hello eksperymentu. W tym momencie eksperymentu powinien wyglądać jak rysunek 5.

![Przy użyciu eksperymentów zip skrypt języka R][6]

*Rysunek 5. Przy użyciu eksperymentów zip skrypt języka R.*

#### <a name="dataset1"></a>Dataset1
Można przekazać prostokątne tabeli danych tooyour R kodu za pomocą hello Dataset1 danych wejściowych. W naszym hello prostego skryptu `maml.mapInputPort(1)` funkcja odczytuje hello dane z portu 1. Te dane jest przypisywana nazwa zmiennej dataframe tooa w kodzie. W naszym prostego skryptu hello pierwszy wiersz kodu wykonuje hello przypisania.

    cadairydata <- maml.mapInputPort(1)

Wykonanie eksperymentu, klikając hello **Uruchom** przycisku. Po zakończeniu wykonywania hello, kliknij polecenie hello [wykonanie skryptu języka R] [ execute-r-script] modułu, a następnie kliknij przycisk **widoku pliku dziennika** w okienku właściwości hello. Nowa strona powinna zostać wyświetlona w przeglądarce przedstawiający hello zawartość pliku dane_wyjściowe.log hello. Podczas przewijania w dół powinien zostać wyświetlony ekran podobny do następujących hello.

    [ModuleOutput] InputDataStructure
    [ModuleOutput]
    [ModuleOutput] {
    [ModuleOutput]  "InputName":Dataset1
    [ModuleOutput]  "Rows":228
    [ModuleOutput]  "Cols":9
    [ModuleOutput]  "ColumnTypes":System.Int32,3,System.Double,5,System.String,1
    [ModuleOutput] }

Dalej w dół hello strona jest bardziej szczegółowe informacje o hello kolumn, które będą wyglądać jak poniżej hello.

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput]
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput]
    [ModuleOutput]  $ Column 0         : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput]
    [ModuleOutput]  $ Year.Month       : num  1995 1995 1995 1995 1995 ...
    [ModuleOutput]
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput]
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput]
    [ModuleOutput]  $ Month            : chr  "Jan" "Feb" "Mar" "Apr" ...
    [ModuleOutput]
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput]
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput]
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput]
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...

Wyniki są przeważnie zgodnie z oczekiwaniami, 228 uwag i 9 kolumn w hello dataframe. Widzimy hello nazwy kolumn, typ danych hello R i przykładowe każdej kolumny.

> [!NOTE]
> Ten sam wydruku jest łatwo dostępne z hello urządzenia R dane wyjściowe hello [wykonanie skryptu języka R] [ execute-r-script] modułu. Omówimy hello elementy wyjściowe hello [wykonanie skryptu języka R] [ execute-r-script] modułu w następnej sekcji hello.  
> 
> 

#### <a name="dataset2"></a>Dataset2
Witaj zachowanie hello Dataset2 danych wejściowych jest identyczne toothat z Dataset1. Przy użyciu tych danych wejściowych można przekazać drugiej tabeli prostokątne danych do kodu języka R. Witaj funkcja `maml.mapInputPort(2)`, z argumentem hello 2, jest używane toopass tych danych.  

### <a name="execute-r-script-outputs"></a>Wykonanie skryptu języka R w danych wyjściowych
#### <a name="output-a-dataframe"></a>Dane wyjściowe dataframe
Można output hello zawartość dataframe R jako tabelę prostokątne za pośrednictwem portu hello Dataset1 wyników przy użyciu hello `maml.mapOutputPort()` funkcji. W naszym prostego skryptu języka R jest to wykonywane przez hello następującego wiersza.

    maml.mapOutputPort('cadairydata')

Po uruchomionych hello eksperymentu, kliknij na powitania port wyjściowy Dataset1 wyników, a następnie kliknij polecenie **Visualize**. Powinny zostać wyświetlone informacje takie jak rysunek 6.

![Hello wizualizację danych wyjściowych hello hello Kalifornijskiej mleczarskich danych][7]

*Rysunek 6. Wizualizacja Hello hello dane wyjściowe hello Kalifornijskiej mleczarskich danych.*

Te dane wyjściowe wygląda toohello identyczne dane wejściowe, dokładnie tak, jak oczekiwaliśmy.  

### <a name="r-device-output"></a>Dane wyjściowe R urządzenia
Witaj urządzenia dane wyjściowe hello [wykonanie skryptu języka R] [ execute-r-script] moduł zawiera dane wyjściowe wiadomości i grafiki. Standardowe Wyjście i błąd standardowy komunikaty o błędach z języka R są wysyłane toohello port wyjściowy R urządzenia.  

Witaj tooview R urządzenia wyjściowego, kliknij na powitania portu, a następnie na **Visualize**. Widzimy hello wyjście standardowe i błąd standardowy ze skryptu hello R na rysunku 7.

![Wyjście standardowe i błąd standardowy z hello portu urządzenia R][8]

*Rysunek 7. Wyjście standardowe i błąd standardowy z hello portu urządzenia R.*

Przewijanie w dół możemy wyświetlić dane wyjściowe grafiki hello z naszych skrypt języka R na rysunku 8.  

![Dane wyjściowe grafiki hello portu urządzenia R][9]

*Rysunek 8. Graficzne dane wyjściowe z hello portu urządzenia R.*  

## <a id="filtering"></a>Filtrowanie danych i przekształcania
W tej sekcji zostaną wykonane niektóre podstawowe dane filtrowania i operacjami transformacji na powitania Kalifornijskiej mleczarskich danych. Końca hello w tej sekcji zostanie zostały dane w formacie odpowiedni w przypadku tworzenia modelu danych analitycznych.  

W szczególności, w tej sekcji zostaną wykonane kilka typowych danych czyszczenia i przekształcenie zadań: wpisz przekształcania filtrowanie dataframes Dodawanie nowej kolumny obliczane, a wartość przekształcenia. Ta tła powinna ułatwić postępowania w przypadku hello wiele zmian w rzeczywistych problemów.

Hello pełną R kodu w tej sekcji znajduje się w pliku zip hello pobrany wcześniej.

### <a name="type-transformations"></a>Typ przekształcenia
Teraz, gdy firma Microsoft może odczytywać hello Kalifornijskiej mleczarskich danych do kodu hello R w hello [wykonanie skryptu języka R] [ execute-r-script] modułu, potrzebujemy tooensure, że dane hello w kolumnach hello ma hello przeznaczony typ i format.  

R jest językiem typach określanych dynamicznie, co oznacza, że typy danych są przekształcone z jednego tooanother zgodnie z wymaganiami. typy danych atomic Hello w R to liczbowe, logicznych i znak. Typ współczynnik Hello jest używane toocompactly przechowywania danych podzielone na kategorie. Znacznie więcej informacji o typach danych można znaleźć w odwołaniach hello w [dodatek B — dalsze informacje](#appendixb).

Podczas odczytywania danych tabelarycznych w R ze źródła zewnętrznego, zawsze jest dobrym rozwiązaniem hello toocheck, co typów w kolumnach hello. Może być kolumną typu znaków, ale w wielu przypadkach to będzie wyświetlany jako współczynnik lub na odwrót. W innych przypadkach kolumny, które zdaniem użytkownika powinna być liczbowe jest reprezentowana przez dane znakowe, np. numer punktu "1,23" zamiast 1,23 jako liczbą zmiennoprzecinkową.  

Na szczęście jest łatwe tooconvert jeden typ tooanother tak długo, jak mapowanie jest możliwe. Na przykład "Nevada" nie można przekonwertować na wartość numeryczną, ale można go przekonwertować współczynnik tooa (podzielone na kategorie zmienna). Inny przykład liczbowe 1 można przekonwertować na znak "1" lub współczynnik.  

żadnego z tych konwersje Hello składnia jest prosty: `as.datatype()`. Te funkcje konwersji typu obejmują następujące hello.

* `as.numeric()`
* `as.character()`
* `as.logical()`
* `as.factor()`

Spojrzenie na powitania typy danych kolumn hello możemy danych wejściowych w poprzedniej sekcji hello: wszystkie kolumny są typu liczbowego, z wyjątkiem hello kolumnę z etykietą "Month", który jest typem znaku. Umożliwia konwertowanie ten współczynnik tooa i hello wyniki testu.  

Usunięto wiersz hello hello scatterplot macierzy i dodawane linii konwertowanie współczynnik tooa kolumny "Month" hello. W moim eksperymencie I będzie tylko wycinanie i wklejanie kodu hello R do okna Kod hello hello [wykonanie skryptu języka R] [ execute-r-script] modułu. Można również zaktualizować hello pliku zip i przekazać go tooAzure Machine Learning Studio, ale trwa to kilka kroków.  

    ## Only one of hello following two lines should be used
    ## If running in Machine Learning Studio, use hello first line with maml.mapInputPort()
    ## If in RStudio, use hello second line with read.csv()
    cadairydata <- maml.mapInputPort(1)
    # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
    ## Ensure hello coding is consistent and convert column tooa factor
    cadairydata$Month <- as.factor(cadairydata$Month)
    str(cadairydata) # Check hello result
    ## hello following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('cadairydata')

Umożliwia wykonanie tego kodu i sprawdź w dzienniku danych wyjściowych hello hello skrypt języka R. Witaj odpowiednich danych z dziennika hello jest pokazano na rysunku 9.

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Column 0         : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year.Month       : num  1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 14 levels "Apr","April",..: 6 5 9 1 11 8 7 3 14 13 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

*Rysunek 9. Podsumowanie dataframe hello ze zmienną Multi-Factor.*

Typ Hello miesiąc teraz zostanie wyświetlony komunikat "**współczynnik z 14 poziomy**". Jest to problem, ponieważ w roku hello są tylko 12 miesięcy. Możesz również sprawdzić toosee, który hello typu w **Visualize** hello wynik Dataset jest port "**Categorical**".

Hello problem jest tym hello "Month", kolumna nie zawiera systematycznie kodowany. W niektórych przypadkach miesiąca nosi kwietnia i w innych jest skracana jako kwietnia. Problem można rozwiązać przez przycinanie znaków too3 ciąg hello. Witaj wiersz kodu teraz wygląda hello:

    ## Ensure hello coding is consistent and convert column tooa factor
    cadairydata$Month <- as.factor(substr(cadairydata$Month, 1, 3))

Ponownie hello eksperyment i wyświetlić hello pliku dziennika. Witaj oczekuje się, że wyniki są wyświetlane na rysunku nr 10.  

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Column 0         : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year.Month       : num  1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

*Rysunek 10. Podsumowanie dataframe hello z poprawną liczbę poziomów współczynnik.*

Nasze zmiennej współczynnik ma teraz hello potrzeby 12 poziomów.

### <a name="basic-data-frame-filtering"></a>Filtrowanie ramki danych podstawowych
R dataframes obsługuje zaawansowane funkcje filtrowania. Zestawy danych mogą być podzbiory przy użyciu filtrów logiczne według wierszy lub kolumn. W wielu przypadkach będzie wymagane kryteria filtrowania złożonych. Witaj odwołania w [dodatek B — dalsze informacje](#appendixb) zawierają przykłady szeroką gamę dataframes filtrowania.  

Istnieje jeden bit filtrowania należy wykonać w naszym zestawie danych. Jeśli przyjrzymy się hello kolumn w hello cadairydata dataframe, zobaczysz dwóch zbędne kolumny. Hello pierwsza kolumna zawiera tylko numer wiersza, który nie jest bardzo przydatne. Witaj drugiej kolumny Year.Month, zawiera nadmiarowych. Firma Microsoft łatwo wykluczyć te kolumny za pomocą hello następującego kodu języka R.

> [!NOTE]
> Od teraz w w tej sekcji zostanie tylko wyświetlić możesz dodatkowy kod dodaję hello hello [wykonanie skryptu języka R] [ execute-r-script] modułu. Dodam każdego nowego wiersza **przed** hello `str()` funkcji. Używać tej funkcji tooverify wyniki w usłudze Azure Machine Learning Studio.
> 
> 

Dodać powitania po wierszu kodu toomy R hello [wykonanie skryptu języka R] [ execute-r-script] modułu.

    # Remove two columns we do not need
    cadairydata <- cadairydata[, c(-1, -2)]

Uruchom ten kod w eksperymencie i sprawdź wynik hello hello pliku dziennika. Wyniki te są wyświetlane w rysunek 11.

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  7 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

*Rysunek 11. Podsumowanie dataframe hello z dwóch kolumn będących jej usunąć.*

Dobre wieści! Uzyskujemy hello oczekiwano wyników.

### <a name="add-a-new-column"></a>Dodaj nową kolumnę
modeli szeregów czasowych toocreate będzie ona wygodne toohave kolumny zawierające hello miesięcy od czasu uruchomienia hello hello szeregów czasowych. Utworzymy nową kolumnę "Month.Count".

toohelp organizowanie kodu hello utworzymy naszych pierwszej funkcji proste `num.month()`. Ta funkcja toocreate nową kolumnę w hello dataframe następnie zostaną zastosowane. Nowy kod Hello ma następującą składnię.

    ## Create a new column with hello month count
    ## Function toofind hello number of months from hello first
    ## month of hello time series
    num.month <- function(Year, Month) {
      ## Find hello starting year
      min.year  <- min(Year)

      ## Compute hello number of months from hello start of hello time series
      12 * (Year - min.year) + Month - 1
    }

    ## Compute hello new column for hello dataframe
    cadairydata$Month.Count <- num.month(cadairydata$Year, cadairydata$Month.Number)

Teraz uruchomić eksperyment hello zaktualizowane i użyć hello danych wyjściowych dziennika tooview hello wyników. W rysunku 12 przedstawiono te wyniki.

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  8 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

*Rysunek 12. Podsumowanie dataframe hello hello dodatkowe kolumny.*

Wygląda na to, wszystko działa. W naszym dataframe zostały hello nową kolumnę z hello oczekiwanych wartości.

### <a name="value-transformations"></a>Przekształcenia wartości
W tej sekcji zostaną wykonane na powitania wartości w niektórych hello kolumn z naszych dataframe niektórych prostych transformacji. język Hello R obsługuje przekształcenia niemal dowolną wartość. Witaj odwołania w [dodatek B — dalsze informacje](#appendixb) zawiera szeroką gamę przykłady.

Jeśli przyjrzymy się hello wartości podsumowań hello naszych dataframe powinny zostać wyświetlone informacje nieparzysta tutaj. Więcej lodów niż mleko jest generowany w Kalifornijskiej? Nie, oczywiście nie, jak to ma sensu sad jako ten fakt może być toosome NAS lovers lodów. jednostki Hello są różne. Cena Hello jest w jednostkach nam kg, mleko jest w jednostkach 1 mln kg USA, lodów znajduje się w jednostkach 1000 nam galonach, i ser chałupniczej jest w jednostce 1000 jednostkach funt Stanów Zjednoczonych. Zakładając, że lodów waga na galon paliwa około jednostkach 6.5 funt, firma Microsoft może łatwo hello tooconvert mnożenia tych wartości, dzięki czemu są one w taki sam jednostek 1000 jednostkach funt.

Dla modelu prognozowania używamy mnożenia modelu trendu i okresach dostosowania tych danych. Transformacja dziennika pozwala nam toouse model liniowy, co upraszcza ten proces. Można zastosować transformacji dziennika hello w hello sam funkcji, których mnożnik hello jest stosowane.

W hello następującego kodu, można zdefiniować nową funkcję, `log.transform()`i zastosować je toohello wiersze zawierające hello wartości liczbowe. Witaj R `Map()` hello tooapply używana jest funkcja `log.transform()` toohello funkcja wybrane kolumny z hello dataframe. `Map()`przypomina zbyt`apply()` , ale zezwala na więcej niż jedną listę argumentów toohello funkcji. Należy pamiętać, że lista mnożników dostarcza hello drugi argument toohello `log.transform()` funkcji. Witaj `na.omit()` funkcji jest używany jako nieco z tooensure oczyszczania nie ma brakujących lub dataframe hello niezdefiniowanej wartości.

    log.transform <- function(invec, multiplier = 1) {
      ## Function for hello transformation, which is hello log
      ## of hello input value times a multiplier

      warningmessages <- c("ERROR: Non-numeric argument encountered in function log.transform",
                           "ERROR: Arguments toofunction log.transform must be greate than zero",
                           "ERROR: Aggurment multiplier toofuncition log.transform must be a scaler",
                           "ERROR: Invalid time seies value encountered in function log.transform"
                           )

      ## Check hello input arguments
      if(!is.numeric(invec) | !is.numeric(multiplier)) {warning(warningmessages[1]); return(NA)}  
      if(any(invec < 0.0) | any(multiplier < 0.0)) {warning(warningmessages[2]); return(NA)}
      if(length(multiplier) != 1) {{warning(warningmessages[3]); return(NA)}}

      ## Wrap hello multiplication in tryCatch
      ## If there is an exception, print hello warningmessage to
      ## standard error and return NA
      tryCatch(log(multiplier * invec),
               error = function(e){warning(warningmessages[4]); NA})
    }


    ## Apply hello transformation function toohello 4 columns
    ## of hello dataframe with production data
    multipliers  <- list(1.0, 6.5, 1000.0, 1000.0)
    cadairydata[, 4:7] <- Map(log.transform, cadairydata[, 4:7], multipliers)

    ## Get rid of any rows with NA values
    cadairydata <- na.omit(cadairydata)  

Występuje dość bitowe w toku w hello `log.transform()` funkcji. Większość tego kodu jest wyszukiwanie potencjalnych problemów z argumentami hello lub zajmujących się wyjątki, które nadal mogą wystąpić podczas hello obliczenia. Tylko kilka wierszy kodu faktycznie hello obliczenia.

Celem Hello programowania obrony hello jest tooprevent hello awarii jednej funkcji, który uniemożliwia przetwarzania przed kontynuowaniem. Niespodziewane błąd analizy długotrwałe może być dość irytujące dla użytkowników. tooavoid, który ograniczy tej sytuacji, domyślne wartości zwracanych musi być wybrana który uszkodzenie toodownstream przetwarzania. Komunikat jest również utworzonych tooalert użytkowników, którzy coś stała się problem.

Jeśli nie jesteś programowania toodefensive używanych w R, ten kod może wydawać się nieco utrudnione. I przeprowadzi Cię przez najważniejsze czynności hello:

1. Wektor cztery komunikaty jest zdefiniowany. Komunikaty te są używane toocommunicate informacji na temat niektórych hello ewentualne błędy i wyjątki, które mogą wystąpić o tym kodzie.
2. I zwróć wartość NA dla każdego przypadku. Istnieje wiele możliwości, które mogą mieć mniej efekty uboczne. Można wrócić wektor wartości zerowe lub hello oryginalnego wektora wejściowych, na przykład.
3. Testy są uruchamiane na hello argumenty toohello funkcji. W każdym przypadku, jeśli zostanie wykryty błąd, zwracana jest wartość domyślna i wiadomość jest generowany przez hello `warning()` funkcji. Używam `warning()` zamiast `stop()` jako ostatnie hello spowoduje przerwanie wykonywania, dokładnie co próbuję tooavoid. Należy pamiętać, że pismo ten kod w stylu procedurach, tak jak w przypadku tego podejścia funkcjonalności sprawiał złożone i zasłoniętej.
4. obliczenia dziennika Hello są ujęte w `tryCatch()` tak, aby wyjątki nie spowoduje zatrzymania niespodziewane tooprocessing. Bez `tryCatch()` większość błędów zgłaszane przez wynik funkcji R w sygnał zatrzymania, która obsługuje tylko dla niej.

Wykonanie tego kodu języka R w eksperymencie i przyjrzeć się hello wydrukowaniu danych wyjściowych w pliku dane_wyjściowe.log hello. Teraz będą widzieć hello przekształcenia wartości hello cztery kolumny w hello dziennika, jak pokazano na rysunku 13.

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  8 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

*Rysunek 13. Podsumowanie hello przekształcenia wartości hello dataframe.*

Firma Microsoft Zobacz zostały przekształcone hello wartości. Teraz mleczności znacznie przekracza wszystkich innych produktu mleczarskiego środowiska produkcyjnego, odwołując się, że teraz czekamy na skali logarytmicznej.

W tym momencie nasze dane jest wyczyszczone, a firma Microsoft są gotowe do niektórych modelowania. Spojrzenie na powitania wizualizacji podsumowanie hello zestaw wyników danych wyjściowych z naszych [wykonanie skryptu języka R] [ execute-r-script] modułu, widoczna tam będzie kolumny "Month" hello "Categorical" 12 unikatowych wartości, ponownie, podobnie jak możemy .

## <a id="timeseries"></a>Obiekty serie czasu i analiza korelacji
W tej sekcji możemy eksplorowania kilka podstawowych obiektów serii czas R i analizować hello korelacji między niektóre zmienne hello. Naszym celem jest toooutput dataframe zawierającego hello Pairwise — informacje o powiązaniu na kilka odchyłki.

Hello pełny kod R dla tej sekcji znajduje się w pliku zip hello pobrany wcześniej.

### <a name="time-series-objects-in-r"></a>Czas obiektów serii R
Jak już wspomniano, czas serii są serii danych wartości indeksowane według czasu. Obiekty serii czas R są używane toocreate i zarządzaj nimi hello czasu indeksu. Ma kilka zalet toousing czasu serii obiektów. Czas serii obiektów Brak hello wielu szczegółów związanych z zarządzaniem hello czasu serii indeks wartości, które znajdują się w obiekcie hello. Ponadto obiekty serii czasu zezwolić toouse hello wiele metod serii czas do kreślenia, drukowanie, modelowania itp.

Hello klasa serii czasu POSIXct to powszechnie używane i jest stosunkowo proste. Ta klasa serii czasu mierzy czas od początku hello epoki hello, 1 stycznia 1970. W tym przykładzie używamy POSIXct czasu serii obiektów. Inne powszechnie używane klasy obiektu serii czas R obejmują zoo i xts, szeregów czasowych rozszerzonego.
<!-- Additional information on R time series objects is provided in hello references in Section 5.7. [commenting because this section doesn't exist, even in hello original] -->

### <a name="time-series-object-example"></a>Przykład obiektu serii czasu
Rozpocznijmy naszym przykładzie. Przeciągnij i upuść **nowe** [wykonanie skryptu języka R] [ execute-r-script] modułu w eksperymencie. Połącz port wyjściowy hello Dataset1 wynik istniejących hello [wykonanie skryptu języka R] [ execute-r-script] portu hello nowych danych wejściowych modułu toohello Dataset1 [wykonanie skryptu języka R] [ execute-r-script] modułu.

Tak jak pierwszy przykłady hello, jak firma Microsoft postępu za pośrednictwem przykład Witaj, w niektórych punktach I będą wyświetlane tylko hello przyrostowe dodatkowe wiersze kodu języka R w każdym kroku.  

#### <a name="reading-hello-dataframe"></a>Odczytywanie hello dataframe
Pierwszym krokiem umożliwia odczytu w dataframe i upewnij się, że uzyskujemy hello oczekiwano wyników. Witaj następujący kod należy wykonać zadania hello.

    # Comment hello following if using RStudio
    cadairydata <- maml.mapInputPort(1)
    str(cadairydata) # Check hello results

Teraz uruchom hello eksperymentu. Dziennik Hello hello nowy kształt wykonanie skryptu języka R powinien wyglądać rysunku 14.

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  8 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...

*Rysunek 14. Podsumowanie dataframe hello w module wykonanie skryptu języka R hello.*

Te dane są hello oczekiwano typu i formatu. Należy zauważyć, że kolumna "Month" hello współczynnika typu i ma hello oczekiwana liczba poziomów.

#### <a name="creating-a-time-series-object"></a>Tworzenie obiektów serii czasu
Potrzebujemy tooadd dataframe tooour czasu serii obiektu. Zastąp bieżący kod hello hello następujący komunikat, który dodaje kolumnę nowej klasy POSIXct.

    # Comment hello following if using RStudio
    cadairydata <- maml.mapInputPort(1)

    ## Create a new column as a POSIXct object
    Sys.setenv(TZ = "PST8PDT")
    cadairydata$Time <- as.POSIXct(strptime(paste(as.character(cadairydata$Year), "-", as.character(cadairydata$Month.Number), "-01 00:00:00", sep = ""), "%Y-%m-%d %H:%M:%S"))

    str(cadairydata) # Check hello results

Teraz Sprawdź dziennik hello. Powinien on wyglądać rys. 15.

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Time             : POSIXct, format: "1995-01-01" "1995-02-01" ...

*Rysunek 15. Podsumowanie dataframe hello z obiektem serii czasu.*

Firma Microsoft może zapoznaj się z hello podsumowania tej nowej kolumny hello jest w rzeczywistości klasy POSIXct.

### <a name="exploring-and-transforming-hello-data"></a>Poznawanie i przekształcanie danych hello
Przyjrzyjmy się niektóre zmienne hello w tym zestawie danych. Macierz scatterplot to dobry sposób tooproduce szybko wyświetlić. Jestem I zastępowanie hello `str()` funkcji w hello poprzedni kod języka R z hello następującego wiersza.

    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata, main = "Pairwise Scatterplots of dairy time series")

Uruchom ten kod i zobacz, co się stanie. kreślenia Hello w hello portu urządzenia R powinien wyglądać rysunek 16.

![Macierz Scatterplot wybranych zmiennych][17]

*Rysunek 16. Macierz Scatterplot wybranych zmiennych.*

Witaj relacji między tymi zmiennymi jest niektórych odd-looking struktury. Prawdopodobnie wynika to z trendów w danych hello i hello fakt, że firma Microsoft nie ustalić hello zmiennych.

### <a name="correlation-analysis"></a>Analiza korelacji
tooperform korelacji analizy potrzebujemy tooboth cofnąć trendów i standaryzowanie hello zmiennych. Firma Microsoft może po prostu użyć hello R `scale()` funkcji, która koncentruje się jak również skaluje zmiennych. Ta funkcja może być również szybsze. Jednak ma tooshow należy zapoznać się przykładem obrony programing w języku R.

Witaj `ts.detrend()` funkcja pokazano poniżej wykonuje obie te operacje. Witaj następujące dwa wiersze kodu cofnąć tendencji hello danych i zapewnij standaryzację hello wartości.

    ts.detrend <- function(ts, Time, min.length = 3){
      ## Function toode-trend and standardize a time series

      ## Define some messages if they are NULL  
      messages <- c('ERROR: ts.detrend requires arguments ts and Time toohave hello same length',
                    'ERROR: ts.detrend requires argument ts toobe of type numeric',
                    paste('WARNING: ts.detrend has encountered a time series with length less than', as.character(min.length)),
                    'ERROR: ts.detrend has encountered a Time argument not of class POSIXct',
                    'ERROR: Detrend regression has failed in ts.detrend',
                    'ERROR: Exception occurred in ts.detrend while standardizing time series in function ts.detrend'
      )
      # Create a vector of zeros tooreturn as a default in some cases
      zerovec  <- rep(length(ts), 0.0)

      # hello input arguments are not of hello same length, return ts and quit
      if(length(Time) != length(ts)) {warning(messages[1]); return(ts)}

      # If hello ts is not numeric, just return a zero vector and quit
      if(!is.numeric(ts)) {warning(messages[2]); return(zerovec)}

      # If hello ts is too short, just return it and quit
      if((ts.length <- length(ts)) < min.length) {warning(messages[3]); return(ts)}

      ## Check that hello Time variable is of class POSIXct
      if(class(cadairydata$Time)[[1]] != "POSIXct") {warning(messages[4]); return(ts)}

      ## De-trend hello time series by using a linear model
      ts.frame  <- data.frame(ts = ts, Time = Time)
      tryCatch({ts <- ts - fitted(lm(ts ~ Time, data = ts.frame))},
               error = function(e){warning(messages[5]); zerovec})

      tryCatch( {stdev <- sqrt(sum((ts - mean(ts))^2))/(ts.length - 1)
                 ts <- ts/stdev},
                error = function(e){warning(messages[6]); zerovec})

      ts
    }  
    ## Apply hello detrend.ts function toohello variables of interest
    df.detrend <- data.frame(lapply(cadairydata[, 4:7], ts.detrend, cadairydata$Time))

    ## Plot hello results toolook at hello relationships
    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = df.detrend, main = "Pairwise Scatterplots of detrended standardized time series")

Występuje dość bitowe w toku w hello `ts.detrend()` funkcji. Większość tego kodu jest wyszukiwanie potencjalnych problemów z argumentami hello lub zajmujących się wyjątki, które nadal mogą wystąpić podczas hello obliczenia. Tylko kilka wierszy kodu faktycznie hello obliczenia.

Już Omówiliśmy przykład obrony Programowanie w [wartości przekształcenia](#valuetransformations). Zarówno bloki obliczenia są ujęte w `tryCatch()`. Niektóre błędy ułatwia oryginalnego wektora wejściowych znaczeniu tooreturn hello, a w pozostałych przypadkach wrócić wektor zer.  

Należy pamiętać, że hello regresji liniowej używane do usuwania analizy trendów regresji serii czasu. Zmienna predykcyjne Hello jest obiekt serii czasu.  

Raz `ts.detrend()` zdefiniowano Trwa stosowanie zmiennych toohello zainteresowanie naszych dataframe. Firma Microsoft musi wymuszone hello wyświetlonej listy utworzone przez `lapply()` dataframe toodata przy użyciu `as.data.frame()`. Z powodu obrony aspektów `ts.detrend()`, popraw tooprocess awarii jednej ze zmiennych hello nie zapobiega przetwarzania hello innych użytkowników.  

Witaj końcowego wiersza kodu tworzy scatterplot parowania. Po uruchomieniu kodu hello R, wyniki hello hello scatterplot są wyświetlane w rysunek 17.

![Scatterplot parowania w szeregu czasowym cofnąć trend i standardowych][18]

*Rysunek 17. Pairwise — scatterplot szeregów czasowych cofnąć trend i standardowych.*

Możesz porównać te toothose wyniki pokazano na rysunku 16. Z hello trend usunięte i hello zmienne standaryzowane, widzimy znacznie mniej strukturze hello relacje między tych zmiennych.

Poniżej przedstawiono Hello kodu toocompute hello korelacji jako obiekty KKS R.

    ## A function toocompute pairwise correlations from a
    ## list of time series value vectors
    pair.cor <- function(pair.ind, ts.list, lag.max = 1, plot = FALSE){
      ccf(ts.list[[pair.ind[1]]], ts.list[[pair.ind[2]]], lag.max = lag.max, plot = plot)
    }

    ## A list of hello pairwise indices
    corpairs <- list(c(1,2), c(1,3), c(1,4), c(2,3), c(2,4), c(3,4))

    ## Compute hello list of ccf objects
    cadairycorrelations <- lapply(corpairs, pair.cor, df.detrend)  

    cadairycorrelations

Uruchomienie tego kodu tworzy dziennika hello pokazano na rysunku 18.

    [ModuleOutput] Loading objects:
    [ModuleOutput]   port1
    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] [[1]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]    -1     0     1 
    [ModuleOutput] 0.148 0.358 0.317 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[2]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]     -1      0      1 
    [ModuleOutput] -0.395 -0.186 -0.238 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[3]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]     -1      0      1 
    [ModuleOutput] -0.059 -0.089 -0.127 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[4]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]    -1     0     1 
    [ModuleOutput] 0.140 0.294 0.293 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[5]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]     -1      0      1 
    [ModuleOutput] -0.002 -0.074 -0.124 

*Rysunek 18. Lista KKS obiektów z hello parowania korelacji analizy.*

Brak wartości korelacji dla każdego opóźnienie. Żaden z tych wartości korelacji nie jest wystarczająco duży toobe znaczące. Firma Microsoft w związku z tym stwierdzić, czy możemy modelu każdej zmiennej niezależnie.

### <a name="output-a-dataframe"></a>Dane wyjściowe dataframe
Firma Microsoft ma obliczana korelacji parowania hello jako listę obiektów KKS R. Przedstawia nieco problem, jako hello port wyjściowy zestaw danych wyników wymaga naprawdę dataframe. Ponadto hello KKS obiekt znajduje się lista i chcemy tylko wartości hello w pierwszym elementem hello tej listy korelacji hello na powitania różnych odchyłki.

Witaj następującego kodu wyodrębnia hello opóźnienie wartości z listy hello KKS obiektów, które są także list.

    df.correlations <- data.frame(do.call(rbind, lapply(cadairycorrelations, '[[', 1)))

    c.names <- c("correlation pair", "-1 lag", "0 lag", "+1 lag")
    r.names  <- c("Corr Cot Cheese - Ice Cream",
                  "Corr Cot Cheese - Milk Prod",
                  "Corr Cot Cheese - Fat Price",
                  "Corr Ice Cream - Mik Prod",
                  "Corr Ice Cream - Fat Price",
                  "Corr Milk Prod - Fat Price")

    ## Build a dataframe with hello row names column and the
    ## correlation data frame and assign hello column names
    outframe <- cbind(r.names, df.correlations)
    colnames(outframe) <- c.names
    outframe


    ## WARNING!
    ## hello following line works only in Azure Machine Learning
    ## When running in RStudio, this code will result in an error
    #maml.mapOutputPort('outframe')

pierwszy wiersz kodu Hello jest nieco trudnych, a niektóre informacje mogą pomóc w go zrozumieć. Praca z hello wewnątrz limit mamy hello następujące czynności:

1. Witaj "**[[**"operator z argumentem hello"**1**" wybiera hello wektor korelacji w odchyłki hello z hello pierwszy element listy obiektów KKS hello.
2. Witaj `do.call()` hello ma zastosowanie funkcja `rbind()` funkcja za pośrednictwem hello elementy listy hello zwraca przez `lapply()`.
3. Witaj `data.frame()` funkcja wymusza traktowanie wyniku hello zwracany przez `do.call()` tooa dataframe.

Należy pamiętać, że hello wiersz nazwy znajdują się w kolumnie hello dataframe. W ten sposób zachowuje hello wiersz nazwy, gdy znajdują się dane wyjściowe hello [wykonanie skryptu języka R][execute-r-script].

Wykonywanie kodu hello hello dane wyjściowe są wyświetlane w rysunek 19 podczas I **wizualizacja** hello dane wyjściowe na powitania portu wynik zestawu danych. Hello wiersz nazwy znajdują się w pierwszej kolumnie hello, zgodnie z założeniami.

![Dane wyjściowe wyniki analizy korelacji hello][20]

*Rysunek 19. Dane wyjściowe z analizy korelacji hello wyniki.*

## <a id="seasonalforecasting"></a>Przykład serii czasu: okresach prognozowania
Naszych danych jest teraz w postaci nadające się do analizy, a Ustaliliśmy, że nie ma żadnych znaczących korelacji między hello zmiennych. Umożliwia przenoszenie na i Utwórz szeregów czasowych, funkcja prognozowania modelu. Użycie tego modelu firma Microsoft będzie prognozy Kalifornijskiej mleczności dla hello 12 miesięcy 2013.

Nasze modelu prognozowania można używać ma dwa składniki, trend składnika i składnik okresach. prognozy pełną Hello jest produktem hello te dwa składniki. Ten typ modelu nosi nazwę modelu mnożenia. Alternatywą Hello jest model dodatku. Zastosowaliśmy ma zainteresowań, co sprawia, że analiza tractable zmiennych toohello przekształcania dziennika.

Hello pełny kod R dla tej sekcji znajduje się w pliku zip hello pobrany wcześniej.

### <a name="creating-hello-dataframe-for-analysis"></a>Tworzenie dataframe hello do analizy
Rozpocznij od dodania **nowe** [wykonanie skryptu języka R] [ execute-r-script] modułu tooyour eksperymentu. Połącz hello **zestaw wyników danych** dane wyjściowe istniejących hello [wykonanie skryptu języka R] [ execute-r-script] toohello modułu **Dataset1** wejściowych hello nowego modułu. wynik Hello powinien wyglądać jak rysunek 20.

![Witaj eksperymentować hello dodany nowy moduł wykonanie skryptu języka R][21]

*Rysunek 20. Witaj eksperymentować hello dodany nowy moduł wykonanie skryptu języka R.*

Jako hello korelacji analizy, które firma Microsoft właśnie został ukończony, potrzebujemy tooadd kolumny z obiektem POSIXct czasu serii. Witaj następującego kodu będzie w tym właśnie.

    # If running in Machine Learning Studio, uncomment hello first line with maml.mapInputPort()
    cadairydata <- maml.mapInputPort(1)

    ## Create a new column as a POSIXct object
    Sys.setenv(TZ = "PST8PDT")
    cadairydata$Time <- as.POSIXct(strptime(paste(as.character(cadairydata$Year), "-", as.character(cadairydata$Month.Number), "-01 00:00:00", sep = ""), "%Y-%m-%d %H:%M:%S"))

    str(cadairydata)

Uruchom ten kod i przyjrzyj się hello dziennika. wynik Hello powinien wyglądać rysunek 21.

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Time             : POSIXct, format: "1995-01-01" "1995-02-01" ...

*Rysunek 21. Podsumowanie hello dataframe.*

Z tym wynikiem są nam gotowe toostart nasze analizy.

### <a name="create-a-training-dataset"></a>Tworzenie zestawu danych szkolenia
Z dataframe hello skonstruowany potrzebujemy toocreate zestawu danych szkoleniowych. Te dane będzie zawierać wszystkie hello uwag, z wyjątkiem hello ostatnie 12 hello roku 2013, czyli naszego zestawu danych testowych. następujące Hello kodu dataframe hello podzestawy i tworzy powierzchni hello mleczarskich zmiennych produkcyjnego i ceny. Utworzyć następnie powierzchni hello produkcyjnego i cen zmiennych. Funkcji anonimowej jest używane toodefine niektórych wspomaga dla powierzchni, a następnie iteracja hello lista hello innych dwa argumenty z `Map()`. Jeśli myślisz, że dla pętli będą działały prawidłowo w tym miejscu, są prawidłowe. Jednak ponieważ funkcjonalności języka R I am zastosowania podejścia funkcjonalności.

    cadairytrain <- cadairydata[1:216, ]

    Ylabs  <- list("Log CA Cotage Cheese Production, 1000s lb",
                   "Log CA Ice Cream Production, 1000s lb",
                   "Log CA Milk Production 1000s lb",
                   "Log North CA Milk Milk Fat Price per 1000 lb")

    Map(function(y, Ylabs){plot(cadairytrain$Time, y, xlab = "Time", ylab = Ylabs, type = "l")}, cadairytrain[, 4:7], Ylabs)

Wykonywanie kodu hello tworzy hello serii szeregów czasowych geograficzne z danych wyjściowych urządzenia R hello pokazano na rysunku 22. Należy pamiętać, że tej osi czasu hello jest wyrażona w jednostkach dat, nieuprzywilejowany korzyści czasu hello metody kreślenia serii.

![Pierwszy z serii wykresy czasu Kalifornijskiej mleczarskich danych produkcyjnych i cen](./media/machine-learning-r-quickstart/unnamed-chunk-161.png)

![Sekundy czasu serii wykresów Kalifornijskiej mleczarskich danych produkcyjnych i cen](./media/machine-learning-r-quickstart/unnamed-chunk-162.png)

![Innych czasu serii wykresów Kalifornijskiej mleczarskich danych produkcyjnych i cen](./media/machine-learning-r-quickstart/unnamed-chunk-163.png)

![Czwarta czasu serii wykresów Kalifornijskiej mleczarskich danych produkcyjnych i cen](./media/machine-learning-r-quickstart/unnamed-chunk-164.png)

*Rysunek 22. Czas serii wykresów mleczarskie Kalifornijskiej i cen danych.*

### <a name="a-trend-model"></a>Wzór trendu
Wytworzeniu obiektów serie czasu i o przyjrzeliśmy danych hello, Zacznijmy tooconstruct wzór trendu hello danych produkcyjnych mleka Polski. Można to zrobić dzięki regresji serii czasu. Jednak jest jasno z hello kreślenia czy firma Microsoft będzie konieczne więcej niż tooaccurately nachylenie i punkt przecięcia modelu hello obserwowanych trendów w danych szkoleniowych hello.

Podana hello małą skalę hello danych, I będzie kompilacji hello wzór trendu w programu RStudio i następnie wycinanie i wklejanie modelu wynikowego hello do usługi Azure Machine Learning. Programu RStudio zapewnia interaktywne środowisko dla tego typu analizy interakcyjnej.

Jako pierwsza próba I ponowi wielomianu regresji uprawnienia się too3. Brak rzeczywistych niebezpieczeństwo nadmiernie dopasowanie tych rodzajów modeli. W związku z tym jest najlepszym tooavoid najwyższego rzędu warunki. Hello `I()` funkcja zapobiega interpretacji hello treści (interpretuje hello zawartość "jak jest") i umożliwia toowrite dosłownie interpretowany funkcja równanie regresji.

    milk.lm <- lm(Milk.Prod ~ Time + I(Month.Count^2) + I(Month.Count^3), data = cadairytrain)
    summary(milk.lm)

Spowoduje to wygenerowanie hello poniżej.

    ##
    ## Call:
    ## lm(formula = Milk.Prod ~ Time + I(Month.Count^2) + I(Month.Count^3),
    ##     data = cadairytrain)
    ##
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max
    ## -0.12667 -0.02730  0.00236  0.02943  0.10586
    ##
    ## Coefficients:
    ##                   Estimate Std. Error t value Pr(>|t|)
    ## (Intercept)       6.33e+00   1.45e-01   43.60   <2e-16 ***
    ## Time              1.63e-09   1.72e-10    9.47   <2e-16 ***
    ## I(Month.Count^2) -1.71e-06   4.89e-06   -0.35    0.726
    ## I(Month.Count^3) -3.24e-08   1.49e-08   -2.17    0.031 *  
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ##
    ## Residual standard error: 0.0418 on 212 degrees of freedom
    ## Multiple R-squared:  0.941,    Adjusted R-squared:  0.94
    ## F-statistic: 1.12e+03 on 3 and 212 DF,  p-value: <2e-16

Z wartości P (Pr (> | t |)) w tym danych wyjściowych widać, że hello kwadratów termin nie może być istotne. Będę używać hello `update()` funkcji toomodify tego modelu przez usunięcie hello kwadrat terminu.

    milk.lm <- update(milk.lm, . ~ . - I(Month.Count^2))
    summary(milk.lm)

Spowoduje to wygenerowanie hello poniżej.

    ##
    ## Call:
    ## lm(formula = Milk.Prod ~ Time + I(Month.Count^3), data = cadairytrain)
    ##
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max
    ## -0.12597 -0.02659  0.00185  0.02963  0.10696
    ##
    ## Coefficients:
    ##                   Estimate Std. Error t value Pr(>|t|)
    ## (Intercept)       6.38e+00   4.07e-02   156.6   <2e-16 ***
    ## Time              1.57e-09   4.32e-11    36.3   <2e-16 ***
    ## I(Month.Count^3) -3.76e-08   2.50e-09   -15.1   <2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ##
    ## Residual standard error: 0.0417 on 213 degrees of freedom
    ## Multiple R-squared:  0.941,  Adjusted R-squared:  0.94
    ## F-statistic: 1.69e+03 on 2 and 213 DF,  p-value: <2e-16

To wygląda lepiej. Wszystkie warunki hello są istotne. Jednak wartość 2e 16 hello wartości domyślnej i nie powinny być pobierane za poważnie.  

Jako test związane z poprawnością upewnijmy wykres serii czasu hello Kalifornijskiej mleczarskie danych z krzywej trend hello wyświetlane. Po dodaniu hello następującego kodu w hello Azure Machine Learning [wykonanie skryptu języka R] [ execute-r-script] toocreate modelu (nie programu RStudio) hello modelu i utworzyć wykres. wynik Hello jest wyświetlany na rysunku 23.

    milk.lm <- lm(Milk.Prod ~ Time + I(Month.Count^3), data = cadairytrain)

    plot(cadairytrain$Time, cadairytrain$Milk.Prod, xlab = "Time", ylab = "Log CA Milk Production 1000s lb", type = "l")
    lines(cadairytrain$Time, predict(milk.lm, cadairytrain), lty = 2, col = 2)

![Danych produkcyjnych mleka Kalifornijskiej z modelem trend pokazano](./media/machine-learning-r-quickstart/unnamed-chunk-18.png)

*Rysunek 23. Polski mleka danych produkcyjnych z modelem trend wyświetlane.*

Wygląda na to, dość dobrze dopasowania modelu trend hello hello danych. Ponadto nie wydaje dowód toobe uwierzytelniając odpowiadający takie jak nietypowych wierci się hello krzywej modelu.  

### <a name="seasonal-model"></a>Okresach modelu
Z modelem trendu w ręcznie firma Microsoft musi mieć toopush na i zawiera efekty okresach hello. Używamy hello miesiąc roku hello jako zmienną fikcyjny obowiązują hello model liniowy toocapture hello kolejnych miesięcy. Należy pamiętać, że podczas wprowadzania współczynnik zmiennych do modelu, hello intercept musi nie można obliczyć. Jeśli nie jest to zrobić, formuła hello jest nadmiernie określonego i R spowoduje porzucenie jedną hello potrzeby czynników, ale zachować hello intercept terminu.

Ponieważ mamy modelu zadowalające trend możemy użyć hello `update()` hello tooadd funkcja nowe warunki toohello istniejącego modelu. Hello -1 w formule aktualizacji hello porzuca hello intercept terminu. Kontynuowanie w programu RStudio chwili hello:

    milk.lm2 <- update(milk.lm, . ~ . + Month - 1)
    summary(milk.lm2)

Spowoduje to wygenerowanie hello poniżej.

    ##
    ## Call:
    ## lm(formula = Milk.Prod ~ Time + I(Month.Count^3) + Month - 1,
    ##     data = cadairytrain)
    ##
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max
    ## -0.06879 -0.01693  0.00346  0.01543  0.08726
    ##
    ## Coefficients:
    ##                   Estimate Std. Error t value Pr(>|t|)
    ## Time              1.57e-09   2.72e-11    57.7   <2e-16 ***
    ## I(Month.Count^3) -3.74e-08   1.57e-09   -23.8   <2e-16 ***
    ## MonthApr          6.40e+00   2.63e-02   243.3   <2e-16 ***
    ## MonthAug          6.38e+00   2.63e-02   242.2   <2e-16 ***
    ## MonthDec          6.38e+00   2.64e-02   241.9   <2e-16 ***
    ## MonthFeb          6.31e+00   2.63e-02   240.1   <2e-16 ***
    ## MonthJan          6.39e+00   2.63e-02   243.1   <2e-16 ***
    ## MonthJul          6.39e+00   2.63e-02   242.6   <2e-16 ***
    ## MonthJun          6.38e+00   2.63e-02   242.4   <2e-16 ***
    ## MonthMar          6.42e+00   2.63e-02   244.2   <2e-16 ***
    ## MonthMay          6.43e+00   2.63e-02   244.3   <2e-16 ***
    ## MonthNov          6.34e+00   2.63e-02   240.6   <2e-16 ***
    ## MonthOct          6.37e+00   2.63e-02   241.8   <2e-16 ***
    ## MonthSep          6.34e+00   2.63e-02   240.6   <2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ##
    ## Residual standard error: 0.0263 on 202 degrees of freedom
    ## Multiple R-squared:     1,    Adjusted R-squared:     1
    ## F-statistic: 1.42e+06 on 14 and 202 DF,  p-value: <2e-16

Widzimy modelu hello już ma termin przechwycenia i ma 12 miesiąca istotne czynniki. Jest to dokładnie co możemy toosee.

Można wprowadzić inny czas serii wykresu hello Kalifornijskiej mleczarskie danych toosee jak działa hello okresach modelu. Po dodaniu hello następującego kodu w hello Azure Machine Learning [wykonanie skryptu języka R] [ execute-r-script] toocreate hello modelu i utworzyć wykres.

    milk.lm2 <- lm(Milk.Prod ~ Time + I(Month.Count^3) + Month - 1, data = cadairytrain)

    plot(cadairytrain$Time, cadairytrain$Milk.Prod, xlab = "Time", ylab = "Log CA Milk Production 1000s lb", type = "l")
    lines(cadairytrain$Time, predict(milk.lm2, cadairytrain), lty = 2, col = 2)

Uruchomienie tego kodu w usłudze Azure Machine Learning tworzy wykres hello pokazano na rysunku 24.

![Polski mleczności z modelu w tym okresach efekty](./media/machine-learning-r-quickstart/unnamed-chunk-20.png)

*Rysunek 24. Polski mleczności z modelu w tym okresach efekty.*

Hello jest raczej wspieranie danych dopasowania toohello pokazano na rysunku 24. Wygląd uzasadnione zarówno hello trend, jak i efekt okresach hello (odmiany miesięczne).

Kolejny test na nasz model umożliwia również przyjrzeć się reszty hello. Hello następujące oblicza kod hello przewidywane wartości z naszych dwa modele, oblicza reszty hello hello okresach modelu i następnie geograficzne pozostałości te hello danych szkoleniowych.

    ## Compute predictions from our models
    predict1  <- predict(milk.lm, cadairydata)
    predict2  <- predict(milk.lm2, cadairydata)

    ## Compute and plot hello residuals
    residuals <- cadairydata$Milk.Prod - predict2
    plot(cadairytrain$Time, residuals[1:216], xlab = "Time", ylab ="Residuals of Seasonal Model")

pozostałe kreślenia Hello jest wyświetlany w 25 rysunku.

![Reszty hello okresach modelu dla danych szkoleniowych hello](./media/machine-learning-r-quickstart/unnamed-chunk-21.png)

*Rysunek 25. Reszty hello okresach modelu dla danych szkoleniowych hello.*

Te składniki resztkowe Szukaj uzasadnione. Brak określonej struktury, jednak uwzględnione hello recesji hello 2008 2009, które bez uwzględnienia nasz model szczególnie dobrze.

pokazano na rysunku 25 kreślenia Hello przydaje się do wykrywania wszelkich wzorce zależnych od czasu w reszty hello. jawne podejście Hello przetwarzania i kreślenia reszty hello, I używać miejsc reszty hello w kolejności czasu na powierzchni hello. Jeśli na powitania drugiej strony I ma wykreślić `milk.lm$residuals`, kreślenia hello nie była w kolejności czasu.

Można również użyć `plot.lm()` tooproduce serii wykresów diagnostycznych.

    ## Show hello diagnostic plots for hello model
    plot(milk.lm2, ask = FALSE)

Ten kod tworzy serii wykresów diagnostycznych pokazano na rysunku 26.

![Pierwszy diagnostycznych powierzchni hello okresach modelu](./media/machine-learning-r-quickstart/unnamed-chunk-221.png)

![Drugi powierzchni diagnostycznych dla modelu okresach hello](./media/machine-learning-r-quickstart/unnamed-chunk-222.png)

![Trzecia diagnostycznych powierzchni hello okresach modelu](./media/machine-learning-r-quickstart/unnamed-chunk-223.png)

![Czwarta diagnostycznych powierzchni hello okresach modelu](./media/machine-learning-r-quickstart/unnamed-chunk-224.png)

*Rysunek 26. Diagnostyka geograficzne hello okresach modelu.*

Istnieje kilka punktów wysokiej znaczenie zidentyfikowany w tych powierzchni, ale nie toocause nas bardzo ważne. Ponadto możemy stwierdzić, z hello normalny Q-Q kreślenia czy reszty hello Zamknij toonormally rozproszonych, ważne założeń modeli liniowych.

### <a name="forecasting-and-model-evaluation"></a>Ocena prognozowania i modelu
Istnieje tylko jeden więcej toocomplete toodo operacją naszym przykładzie. Firma Microsoft konieczne toocompute prognozy i pomiar błąd hello względem hello rzeczywiste dane. Nasze prognozy będą hello 12 miesięcy 2013. Firma Microsoft może obliczeniowe miary błąd dla tych danych rzeczywistych toohello prognozy, który nie jest częścią naszego zestawu danych szkoleniowych. Ponadto firma Microsoft porównanie wydajności na powitania 18 lat toohello danych szkoleniowych 12 miesięcy od danych testowych.  

Używane są liczby metryk wydajności hello toomeasure modeli szeregów czasowych. W tym przypadku użyjemy hello błędu głównego średniej kwadratowej (RMS). Witaj następująca funkcja oblicza błąd hello RMS między dwóch serii.  

    RMS.error <- function(series1, series2, is.log = TRUE, min.length = 2){
      ## Function toocompute hello RMS error or difference between two
      ## series or vectors

      messages <- c("ERROR: Input arguments toofunction RMS.error of wrong type encountered",
                    "ERROR: Input vector toofunction RMS.error is too short",
                    "ERROR: Input vectors toofunction RMS.error must be of same length",
                    "WARNING: Funtion rms.error has received invald input time series.")

      ## Check hello arguments
      if(!is.numeric(series1) | !is.numeric(series2) | !is.logical(is.log) | !is.numeric(min.length)) {
        warning(messages[1])
        return(NA)}

      if(length(series1) < min.length) {
        warning(messages[2])
        return(NA)}

      if((length(series1) != length(series2))) {
           warning(messages[3])
        return(NA)}

      ## If is.log is TRUE exponentiate hello values, else just copy
      if(is.log) {
        tryCatch( {
          temp1 <- exp(series1)
          temp2 <- exp(series2) },
          error = function(e){warning(messages[4]); NA}
        )
      } else {
        temp1 <- series1
        temp2 <- series2
      }

     ## Compute predictions from our models
    predict1  <- predict(milk.lm, cadairydata)
    predict2  <- predict(milk.lm2, cadairydata)

    ## Compute hello RMS error in a dataframe
      tryCatch( {
        sqrt(sum((temp1 - temp2)^2) / length(temp1))},
        error = function(e){warning(messages[4]); NA})
    }

Jak hello `log.transform()` funkcja omówiono w Witaj "Wartość przekształcenia" sekcji, jest bardzo dużo kod błędu sprawdzania i wyjątków odzyskiwania w tej funkcji. zastosować zasady Hello są hello tego samego. Witaj praca odbywa się w dwóch miejscach w `tryCatch()`. Najpierw szeregów czasowych hello są exponentiated, ponieważ firma Microsoft odbywała się wcześniej Praca z dziennikami hello hello wartości. Po drugie błędu RMS hello jest kolumną obliczaną.  

Załóżmy wyposażony hello toomeasure funkcja błędu RMS, kompilacji i wyjściowych dataframe, zawierające błędy hello usługi RMS. Firma Microsoft będzie zawierać warunki dla samego modelu trend hello i hello pełny model o okresach czynników. Witaj następujący kod hello zadania przy użyciu hello dwa liniowej modele, które firma Microsoft ma być skonstruowany.

    ## Compute hello RMS error in a dataframe
    ## Include hello row names in hello first column so they will
    ## appear in hello output of hello Execute R Script
    RMS.df  <-  data.frame(
    rowNames = c("Trend Model", "Seasonal Model"),
      Traing = c(
      RMS.error(predict1[1:216], cadairydata$Milk.Prod[1:216]),
      RMS.error(predict2[1:216], cadairydata$Milk.Prod[1:216])),
      Forecast = c(
        RMS.error(predict1[217:228], cadairydata$Milk.Prod[217:228]),
        RMS.error(predict2[217:228], cadairydata$Milk.Prod[217:228]))
    )
    RMS.df

    ## hello following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('RMS.df')

Uruchomienie tego kodu generuje hello dane wyjściowe pokazano rysunek 27 na powitania port wyjściowy zestaw danych z wyników.

![Porównanie usług RMS błędów dla modeli hello][26]

*Rysunek 27. Porównanie błędy usług RMS dla modeli hello.*

Z tymi wynikami widzimy, że dodawanie hello okresach czynniki toohello model zmniejsza błędu RMS hello znacznie. Nie za zaskakująco hello RMS błąd hello szkolenia danych bit jest mniejsza niż dla hello prognozy.

## <a id="appendixa"></a>Dodatek A: Przewodnik tooRStudio
Programu RStudio jest bardzo dobrze udokumentowane, więc w tym dodatku I zapewni niektórych toohello łącza kluczowe sekcje tooget dokumentacji programu RStudio hello, uruchamiany.

1. Tworzenie projektów
   
   Można porządkować i zarządzać kodem R do projektów przy użyciu programu RStudio. w dokumentacji Hello używa projektów znajduje się w temacie https://support.rstudio.com/hc/articles/200526207-Using-Projects.
   
   Najlepiej wykonać te kroki, a następnie utwórz projekt hello R przykłady kodu w tym dokumencie.  
2. Edytowanie i wykonywanie kodu języka R
   
   Programu RStudio zapewnia zintegrowane środowisko umożliwiające edytowanie i wykonywanie kodu języka R. Dokumentację można znaleźć w https://support.rstudio.com/hc/articles/200484448-Editing-and-Executing-Code.
3. Debugowanie
   
   Programu RStudio obejmuje zaawansowane możliwości debugowania. Dokumentacja dla tych funkcji jest na https://support.rstudio.com/hc/articles/200713843-Debugging-with-RStudio.
   
   funkcje rozwiązywania punktu przerwania Hello są udokumentowane w https://support.rstudio.com/hc/articles/200534337-Breakpoint-Troubleshooting.

## <a id="appendixb"></a>Dodatek B: Dalsze informacje.
R, ten samouczek obejmuje hello podstawy programowania z jakich należy toouse hello języka R w usłudze Azure Machine Learning Studio. Jeśli nie masz doświadczenia w obsłudze R, dwie instrukcje są dostępne w sieci CRAN:

* R dla początkujących przez Emmanuel Paradis jest toostart dobrym miejscem, w http://cran.r-project.org/doc/contrib/Paradis-rdebuts_en.pdf.  
* TooR wprowadzenie przez W. N. Venables et. Al. Przechodzi nieco bardziej szczegółowo w http://cran.r-project.org/doc/manuals/R-intro.html.

Istnieje wiele — książki na R, które mogą pomóc Ci rozpocząć. Poniżej przedstawiono kilka, które mogę być przydatne:

* Witaj grafikę programowania R: A samouczek z oprogramowania statystycznie przez Matloff Normanowi jest tooprogramming znakomity wprowadzenie w języku R.  
* R Cookbook przez Teetor Pawła zapewnia problemu i rozwiązanie podejście toousing R.  
* R w akcji Robert Kabacoff jest innym przydatne książki wstępne. Hello pomocnika szybkie R witryny sieci Web jest zasobem przydatne w http://www.statmethods.net/.
* R Inferno przez oparzenia Patrick jest zaskakująco żartobliwy książki, która zajmuje się liczbę trudnych i trudne tematy, które mogą wystąpić, gdy Programowanie w książce R. hello jest dostępny bezpłatnie na http://www.burns-stat.com/documents/books/the-r-inferno/.
* Jeśli chcesz nowości w zaawansowanych tematów w R mają wygląd książki hello zaawansowane R przez Hadley Wickham. Witaj wersję online tego podręcznika jest dostępny bezpłatnie na http://adv-r.had.co.nz/.

Katalog R czasu serii pakietów można znaleźć w hello widoku zadań sieci CRAN do analizy serii czasowych: http://cran.r-project.org/web/views/TimeSeries.html. Informacje w określonym czasie serii obiektu pakietów należy zapoznać się toohello dokumentacji dla tego pakietu.

Książka Hello wprowadzające szeregu czasowego z R Cowpertwait Pawła i Andrew Metcalfe zawiera R toousing wprowadzenie do analizy serii czasowych. Wiele więcej teoretycznego teksty zawierają przykłady R.

Niektóre dużą zasobów internetowych:

* DataCamp: DataCamp szkoleniowcem R wygodna hello przeglądarki z lekcje wideo i kodowania ćwiczeń. Brak interaktywnych samouczków na powitania najnowsze techniki R i pakietów. Podjęcie wolnego interaktywnego samouczka R hello na https://www.datacamp.com/courses/introduction-to-r
* Przewodnik po uzyskiwanie uruchomiony z R z Programiz https://www.programiz.com/r-programming
* Zawiera krótki samouczek R przez czarne Kelly z http://www.cyclismo.org/tutorial/R/ Clarkson University
* R zasobów 60 + wymienionych w http://www.computerworld.com/article/2497464/business-intelligence-60-r-resources-to-improve-your-data-skills.html

<!--Image references-->
[1]: ./media/machine-learning-r-quickstart/fig1.png
[2]: ./media/machine-learning-r-quickstart/fig2.png
[3]: ./media/machine-learning-r-quickstart/fig3.png
[4]: ./media/machine-learning-r-quickstart/fig4.png
[5]: ./media/machine-learning-r-quickstart/fig5.png
[6]: ./media/machine-learning-r-quickstart/fig6.png
[7]: ./media/machine-learning-r-quickstart/fig7.png
[8]: ./media/machine-learning-r-quickstart/fig8.png
[9]: ./media/machine-learning-r-quickstart/fig9.png
[10]: ./media/machine-learning-r-quickstart/fig10.png
[11]: ./media/machine-learning-r-quickstart/fig11.png
[12]: ./media/machine-learning-r-quickstart/fig12.png
[13]: ./media/machine-learning-r-quickstart/fig13.png
[14]: ./media/machine-learning-r-quickstart/fig14.png
[15]: ./media/machine-learning-r-quickstart/fig15.png
[16]: ./media/machine-learning-r-quickstart/fig16.png
[17]: ./media/machine-learning-r-quickstart/fig17.png
[18]: ./media/machine-learning-r-quickstart/fig18.png
[19]: ./media/machine-learning-r-quickstart/fig19.png
[20]: ./media/machine-learning-r-quickstart/fig20.png
[21]: ./media/machine-learning-r-quickstart/fig21.png
[22]: ./media/machine-learning-r-quickstart/fig22.png

[26]: ./media/machine-learning-r-quickstart/fig26.png

<!--links-->
[appendixa]: #appendixa
[download]: https://azurebigdatatutorials.blob.core.windows.net/rquickstart/RFiles.zip


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
