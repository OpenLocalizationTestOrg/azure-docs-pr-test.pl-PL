---
title: "aaaFeature inżynieryjne i zaznaczenie w usłudze Azure Machine Learning | Dokumentacja firmy Microsoft"
description: "Wyjaśniono celów hello funkcji wybór i inżynieria funkcji oraz przykłady ich roli w procesie rozszerzenie danych hello uczenia maszynowego."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 9ceb524d-842e-4f77-9eae-a18e599442d6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/18/2017
ms.author: zhangya;bradsev
ROBOTS: NOINDEX
redirect_url: machine-learning-data-science-create-features
redirect_document_id: True
ms.openlocfilehash: e3e59329bf46f334396f5975b4e656137362d7ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="feature-engineering-and-selection-in-azure-machine-learning"></a>Inżynieria i wybór funkcji w usłudze Azure Machine Learning
W tym temacie wyjaśniono celów hello funkcji inżynieryjne i wybór funkcji w procesie rozszerzenie danych hello uczenia maszynowego. Przedstawia on procesy te obejmują za pomocą przykładów udostępniane przez usługi Azure Machine Learning Studio.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

dane szkoleniowe Hello używane w uczeniu maszynowym często można zwiększyć przez zaznaczenie hello lub wyodrębniania funkcji z hello nieprzetworzone dane zebrane. Przykład funkcji odtworzone w kontekście hello learning, jak obrazy hello tooclassify odręcznie znaków jest mapy bitowej gęstość utworzone na podstawie danych dystrybucji raw bit hello. Ta mapa można lokalizowania krawędzi hello znaków hello wydajniej hello dystrybucji raw.

Funkcje odtworzone i wybranych zwiększenia efektywności hello hello szkolenia procesu, który próbuje tooextract hello najważniejsze informacje zawarte w danych hello. One również poprawić zasilania hello te modele tooclassify hello danych wejściowych dokładnie i wyniki toopredict odsetek więcej niezawodnie. Funkcja inżynieryjne i wyboru można także połączyć learning hello toomake więcej praktyce tractable. Robi to przez rozszerzanie i następnie zmniejszeniu liczby hello funkcje wymagane toocalibrate lub train model. Ze sobą matematycznie rzecz biorąc, model hello tootrain wybrane funkcje hello są minimalny zbiór zmienne niezależne, hello wzorce w danych hello wyjaśnienia, które następnie pomyślnie przewidywania wyników.

Witaj inżynieryjne i wybór funkcji jest częścią większego procesu, które zwykle obejmuje cztery kroki:

* Zbieranie danych
* Rozszerzenie danych
* Konstruowania modelu
* Przetwarzanie końcowe

Inżynieryjne i wybór tworzą kroku rozszerzenie danych hello uczenia maszynowego. Trzy aspekty tego procesu można wyróżnić dla naszych celów:

* **Przetwarzanie wstępne danych**: tego procesu tooensure prób, które hello zebranych danych jest czysty i spójne. Zawiera zadania, takie jak integrowanie wiele zestawów danych, obsługa brakujące dane, obsługa niespójne dane i konwertowanie typów danych.
* **Inżynieria**: ten proces próbuje toocreate dodatkowe istotne cechy z istniejących funkcji hello w hello danych i tooincrease power predykcyjnej toohello Algorytm uczenia raw.
* **Wybór funkcji**: tego procesu wybiera hello klucza podzbiór oryginalne dane funkcji tooreduce hello wymiarach hello szkolenia problemu.

W tym temacie omówiono tylko hello funkcji inżynieryjne i funkcji wyboru aspektów hello danych ulepszenie procesu. Aby uzyskać więcej informacji na powitania danych przetwarzania wstępnego kroku, zobacz [wstępne przetworzenie danych w usłudze Azure Machine Learning Studio](https://azure.microsoft.com/documentation/videos/preprocessing-data-in-azure-ml-studio/).

## <a name="creating-features-from-your-data--feature-engineering"></a>Tworzenie funkcji z danych--Inżynieria
dane szkoleniowe Hello składa się z macierzy składa się z przykładami (rekordy lub obserwacji przechowywane w wierszach), z których każda ma zestaw funkcji (zmienne lub pól przechowywane w kolumnach). Funkcje Hello określony w projekcie doświadczenia hello są oczekiwane toocharacterize hello wzorce w danych hello. Mimo że wiele hello pierwotnych danych, pola, które mogą zostać bezpośrednio włączone w hello tootrain zestaw używany wybranej funkcji modelu, dodatkowe funkcje odtworzone często muszą toobe utworzone na podstawie hello funkcje hello toogenerate nieprzetworzone dane rozszerzone szkoleniowy zestaw danych.

Jakiego rodzaju funkcje należy utworzyć zestaw danych hello tooenhance podczas uczenia modelu? Odtworzone funkcji, które zwiększają szkolenia hello dostarczają informacji lepiej odróżniającą hello wzorce w danych hello. Spodziewasz się hello nowe funkcje tooprovide dodatkowe informacje, które nie jest wyraźnie przechwycony lub łatwo widoczna w oryginalnym hello lub zestaw istniejących funkcji, ale ten proces jest coś grafiki. Decyzje dźwięku i produktywności często wymagają doświadczenia z niektórych domen.

Podczas uruchamiania przy użyciu usługi Azure Machine Learning, jest najprostszym toograsp ten proces, używając konkretnie przykłady podane w usłudze Machine Learning Studio. Poniżej przedstawiono dwa przykłady:

* Przykład regresji ([prognozowania hello liczby dzierżawy roweru](http://gallery.cortanaintelligence.com/Experiment/Regression-Demand-estimation-4)) w nadzorowanym eksperymentu, gdzie są znane wartości docelowych hello
* Używając przykład klasyfikacji wyszukiwania tekstu [Tworzenie skrótu funkcji][feature-hashing]

### <a name="example-1-adding-temporal-features-for-a-regression-model"></a>Przykład 1: Dodawanie funkcji danych czasowych dla modelu regresji
toodemonstrate jak tooengineer funkcje zadania regresji Użyjmy hello eksperymentu "żądanie prognozowania rowerów" w usłudze Azure Machine Learning Studio. Celem tego eksperymentu Hello jest toopredict hello popytu na powitania rowerów, to znaczy hello numer roweru dzierżawy w określonym miesiącu, dzień lub godzinę. zestaw danych Hello **UCI wynajem roweru zestawu danych** służy jako hello nieprzetworzone dane wejściowe.

Ten zestaw danych jest oparty na prawdziwe dane z hello Bikeshare kapitału firmy, która obsługuje sieci wynajem roweru w stanie Waszyngton kontrolera domeny w hello Stanów Zjednoczonych. zestaw danych Hello reprezentuje liczbę hello roweru dzierżawy w ciągu określonej godziny, dnia, 2011 too2012 i zawiera 17379 wierszy i kolumn 17. zestaw funkcji raw Hello zawiera pogodą (temperatury, wilgotności, szybkość knie) i typ hello dnia hello (święta lub dzień tygodnia). toopredict pola Hello jest **cnt**, liczba reprezentująca hello roweru dzierżawy w ciągu godziny określonych i który od 1 too977.

cztery modele regresji tooconstruct skuteczne funkcje dane szkoleniowe hello, są tworzone za pomocą hello samego algorytmu, ale z czterech różnych szkolenia danych ustawia. Hello cztery zestawy danych reprezentują hello tego samego pierwotnych danych wejściowych, ale z coraz więcej funkcji ustawiona. Te funkcje są podzielone na kategorie cztery:

1. A = pogody + świątecznych dzień tygodnia + weekendowe funkcje hello przewidywane dzień
2. B = liczba rowerów, które zostały dzierżawione w każdym hello ostatnich 12 godzin
3. C = Liczba rowerów, które zostały dzierżawione w każdym hello poprzednich dni 12 na powitania sam godzinę
4. D = liczba rowerów, które zostały dzierżawione w każdym hello poprzednich 12 tygodni na powitania sam godzinę i hello tego samego dnia

Oprócz A zestaw funkcji, który już istnieje w oryginalnych danych pierwotnych hello, hello innych trzy zestawy funkcji są tworzone za pomocą funkcji hello inżynierii procesu. Ostatnie Żądanie hello B przechwytywania dla rowerów hello zestaw funkcji. Skonfigurować funkcji przechwytywania C hello żądanie dla rowerów o określonej godzinie. Funkcja ustawiona D przechwytywania żądanie dla rowerów w określonej godziny i dnia tygodnia hello. Każdy z zestawów danych szkoleniowych hello czterech obejmuje zestawy funkcji A, A + B + C, A + B i A + B + C + D odpowiednio.

W hello eksperymentu uczenia maszynowego Azure te cztery zestawy danych szkoleniowych są tworzone za pomocą czterech oddziałów z zestawu wstępnie przetworzonych danych wejściowych hello. Z wyjątkiem hello lewej strony gałęzi, każdy z tych oddziałów zawiera [wykonanie skryptu języka R] [ execute-r-script] modułu, w którym zestaw pochodnych funkcji (funkcja ustawia B, C i D) jest odpowiednio skonstruowane i toohello zaimportowany zestaw danych. powitania po rysunku przedstawiono skrypt hello R używany zestaw funkcji toocreate B w drugim gałęzi po lewej stronie powitania.

![Utwórz zestaw funkcji](./media/machine-learning-feature-selection-and-engineering/addFeature-Rscripts.png)

Witaj Poniższa tabela zawiera podsumowanie porównania hello wyniki wydajności hello hello cztery modele. Witaj najlepsze wyniki są wyświetlane przez funkcje A + B + C. Należy pamiętać, że w tym częstotliwość błędów hello zmniejsza uwzględniona w danych szkoleniowych hello zestawy dodatkowych funkcji. Zweryfikuje naszych założenie, że zestawy funkcji, które B i C znajdują się dodatkowe informacje istotne dla zadania regresji hello hello. Dodawanie zestawu funkcji hello D nie wydaje się tooprovide każde dodatkowe zmniejszenie hello współczynnik błędów.

![Porównaj wyniki wydajności](./media/machine-learning-feature-selection-and-engineering/result1.png)

### <a name="example2"></a>Przykład 2: Tworzenie funkcji wyszukiwania tekstu
Funkcja engineering jest powszechnie stosowane w tootext powiązanych zadań wyszukiwania, takich jak analiza dokumentu klasyfikacji i wskaźniki nastrojów klientów. Na przykład można tooclassify dokumentów na kilka kategorii typowych założeń jest możliwość hello słów ani fraz uwzględnione w jednym dokumencie kategorii toooccur mniej prawdopodobne w innej kategorii dokumentu. Innymi słowy częstotliwość hello dystrybucji wyraz lub frazę hello jest możliwe toocharacterize innego dokumentu kategorii. W aplikacjach wyszukiwania tekstu funkcja hello inżynierii procesu jest toocreate wymagane funkcje hello dotyczące częstotliwości wyraz lub frazę, ponieważ pojedynczych zawartość tekstową zwykle służą jako hello danych wejściowych.

tooachieve to zadanie, technika o nazwie *Tworzenie skrótu funkcji* jest stosowane tooefficiently Włącz funkcje dowolnego tekstu do indeksów. Zamiast kojarzenie każdego tekstu funkcji (słów ani fraz) tooa określonego indeksu, to funkcje — metoda przy zastosowaniu funkcji toohello funkcji skrótu i za pomocą wartości skrótu jako indeksy bezpośrednio.

W usłudze Azure Machine Learning [Tworzenie skrótu funkcji] [ feature-hashing] moduł, który tworzy te funkcje wyraz lub frazę. Witaj poniższej ilustracji przedstawiono przykład za pomocą tego modułu. zestaw danych wejściowych Hello zawiera dwie kolumny: hello książki klasyfikacji zakresu od 1 too5 i hello rzeczywiste przeglądu zawartości. Celem Hello to [Tworzenie skrótu funkcji] [ feature-hashing] tooretrieve nowe funkcje, które Pokaż częstotliwość wystąpienie hello hello odpowiednich słów ani fraz w ramach przeglądu wybranej książki hello jest moduł. toouse tego modułu należy hello toocomplete następujące kroki:

1. Witaj wybierz kolumnę, która zawiera tekst wejściowy hello (**Col2** w tym przykładzie).
2. Ustaw *mieszania bitsize* too8, czyli 2 ^ 8 = 256 funkcje są tworzone. Witaj wyraz lub frazę w tekście hello jest następnie too256 indeksów skrótu. Witaj parametru *mieszania bitsize* może się wahać od 1 too31. Jeśli parametr hello jest ustawiony tooa dłuższych numerów, hello wyrazów lub wyrażenia jest mniej prawdopodobne toobe skrótu do hello sam indeksu.
3. Ustaw parametr hello *N-gramów* too2. Częstotliwość wystąpienie hello unigrams (funkcja dla każdego pojedynczego wyrazu) i bigrams (funkcja dla każdej pary słów sąsiadujące) to pobiera z hello wejściowego tekstu. Witaj parametru *N-gramów* może się wahać od 0 too10, wskazującą maksymalną liczbę toobe sekwencyjnych słowa objęte funkcją hello.  

![Funkcja wyznaczania wartości skrótu modułu](./media/machine-learning-feature-selection-and-engineering/feature-Hashing1.png)

Witaj poniższej ilustracji przedstawiono wygląd te nowe funkcje.

![Przykład skrótu funkcji](./media/machine-learning-feature-selection-and-engineering/feature-Hashing2.png)

## <a name="filtering-features-from-your-data--feature-selection"></a>Funkcje filtrowania danych — Wybieranie funkcji
*Wybór funkcji* jest proces, który jest powszechnie stosowane konstrukcji toohello zbiorów danych szkoleniowych modelowania predykcyjnego zadań, takich jak zadania klasyfikacji lub regresji. Celem Hello jest tooselect podzbiór funkcji hello z hello oryginalnego zestawu danych, który zmniejsza jej wymiarów przy użyciu minimalny zestaw funkcji toorepresent hello maksymalną ilość wariancji w hello danych. Ten podzestaw funkcji zawiera hello tylko funkcje uwzględnione toobe tootrain hello modelu. Wybór funkcji służy dwa główne cele:

* Wybór funkcji często zwiększa dokładność klasyfikacji przez wyeliminowanie nie ma znaczenia, nadmiarowe lub ściśle powiązane funkcje.
* Funkcja wyboru spadku hello wiele funkcji, która sprawia, że proces uczenia modelu hello jest bardziej wydajne. Jest to szczególnie ważne w przypadku uczących będących tootrain kosztowne, takich jak obsługa wektor maszyny.

Mimo że wybór funkcji wymaga tooreduce hello liczbę funkcji hello zestawu danych używanego tootrain hello modelu, nie jest zazwyczaj określana termin hello tooby *redukcji wymiary.* Metody wyboru funkcji Wyodrębnij podzbiór funkcji oryginalnego hello danych bez konieczności ich zmieniania.  Wymiary metod redukcji stosować odtworzone funkcje, które można przekształcić funkcji oryginalnego hello i w związku z tym ich modyfikować. Przykładami metod redukcji wymiary analizy głównych składników, analiza canonical korelacji i dekompozycji pojedynczej wartości.

Jedną z powszechnie stosowanych kategorii metody wyboru funkcji w kontekście nadzorowany jest wybór funkcji na podstawie filtru. Wyniku obliczenia hello korelacja poszczególnych funkcji i hello atrybut target, te metody mają zastosowanie tooassign statystyczne miary funkcji tooeach wynik. Witaj funkcje są następnie uporządkowane według hello wynik, który można użyć tooset hello próg utrzymywanie lub wyeliminowanie określonych funkcji. Przykładami hello miar statystyczne w tych metod korelacji wariancji x, wzajemne informacji i hello. test chi kwadrat.

Azure Machine Learning Studio udostępnia moduły wybór funkcji. Jak pokazano na następującej ilustracji hello, te moduły obejmują [na podstawie filtru wybór funkcji] [ filter-based-feature-selection] i [analiza liniowa Discriminant Fishera] [ fisher-linear-discriminant-analysis].

![Przykład wybór funkcji](./media/machine-learning-feature-selection-and-engineering/feature-Selection.png)

Na przykład użyć hello [na podstawie filtru wybór funkcji] [ filter-based-feature-selection] moduł przykład wyszukiwania tekstu hello opisane wcześniej. Domyślnym wariantem toobuild modelu regresji po utworzeniu zestaw funkcji 256 za pośrednictwem hello [Tworzenie skrótu funkcji] [ feature-hashing] modułu i zmiennej odpowiedzi hello jest **Col1**i przejrzyj reprezentuje książkę klasyfikacji zakresu od 1 too5. Ustaw **funkcji oceniania metody** zbyt**korelacji wariancji x**, **kolumny docelowej** zbyt**Col1**, i **żądaną liczbę Funkcje** za**50**. Moduł Hello [na podstawie filtru wybór funkcji] [ filter-based-feature-selection] spowoduje utworzenie zestawu danych zawierającego 50 funkcji z atrybut target hello **Col1**. Witaj następujący rysunek przedstawia przepływ hello tego eksperymentu i hello parametrów wejściowych.

![Przykład wybór funkcji](./media/machine-learning-feature-selection-and-engineering/feature-Selection1.png)

Witaj poniższej ilustracji przedstawiono hello wynikowych zestawów danych. Każdej funkcji są oceniane na podstawie na powitania wariancji x korelacji między sobą i hello atrybut target **Col1**. Funkcje Hello z najwyższym wyniki są zachowywane.

![Zestawy danych funkcję Filtr na podstawie zaznaczenia](./media/machine-learning-feature-selection-and-engineering/feature-Selection2.png)

powitania po rysunek przedstawia hello odpowiednie wyniki hello wybrane funkcje.

![Wyniki wybranej funkcji](./media/machine-learning-feature-selection-and-engineering/feature-Selection3.png)

Stosując to [na podstawie filtru wybór funkcji] [ filter-based-feature-selection] modułu, 50 poza 256 funkcje są wybrane, ponieważ mają one hello większość funkcji skorelowane z Zmienna docelowa hello **Col1** oparte na powitania oceniania metody **korelacji wariancji x**.

## <a name="conclusion"></a>Podsumowanie
Funkcja inżynieryjne i wybór funkcji to wykonać dwie czynności wykonywanych dane szkoleniowe hello tooprepare podczas tworzenia modelu uczenia maszynowego. Normalnie engineering funkcji jest zastosowane pierwszy toogenerate funkcje dodatkowe, a następnie kroku wybierania funkcji hello jest wykonywane tooeliminate nie ma znaczenia, nadmiarowe lub funkcje wysokiej skorelowane.

Nie zawsze jest zawsze tooperform funkcji engineering lub funkcji wyboru cech. Określa, czy jest potrzebna, zależy od danych hello ma lub zbierać hello algorytmu, który można wybrać i hello cel hello eksperymentu.

<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[feature-hashing]: https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/
[filter-based-feature-selection]: https://msdn.microsoft.com/library/azure/918b356b-045c-412b-aa12-94a1d2dad90f/
[fisher-linear-discriminant-analysis]: https://msdn.microsoft.com/library/azure/dcaab0b2-59ca-4bec-bb66-79fd23540080/
