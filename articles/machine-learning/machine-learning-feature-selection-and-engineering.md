---
title: "Funkcja inżynieryjne i zaznaczenie w usłudze Azure Machine Learning | Dokumentacja firmy Microsoft"
description: "Wyjaśnia na potrzeby funkcji wybór i inżynieria funkcji i przykłady ich roli w procesie rozszerzenie danych usługi machine learning."
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
redirect_document_id: TRUE
ms.openlocfilehash: 51a5d8fed492cb9301e048c2b6a721e4573a47d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="feature-engineering-and-selection-in-azure-machine-learning"></a>Inżynieria i wybór funkcji w usłudze Azure Machine Learning
W tym temacie opisano na potrzeby funkcji inżynieryjne i wybór funkcji w procesie rozszerzenie danych usługi machine learning. Przedstawia on procesy te obejmują za pomocą przykładów udostępniane przez usługi Azure Machine Learning Studio.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Dane szkoleniowe używane w uczeniu maszynowym często można zwiększyć przez zaznaczenie lub wyodrębniania funkcji w zebranych danych pierwotnych. Przykładem funkcji odtworzone w kontekście obrazów znaków odręcznie klasyfikowania uczenia jest mapy bitowej gęstość zbudowane z bitowego nieprzetworzone dane dystrybucji. Ta mapa można lokalizowania krawędzi znaki wydajniej dystrybucji raw.

Odtworzone i wybranych funkcji zwiększyć wydajność procesu szkolenia, która podejmuje próbę wyodrębnić klucza informacje zawarte w danych. Poprawiają również uprawnienia tych modeli dokładnie klasyfikowania danych wejściowych oraz do przewidywania wyników odsetek bardziej niezawodnie. Funkcja inżynieryjne i wyboru można także połączyć dokonanie więcej praktyce tractable learning. Robi to udoskonalanie, a następnie zmniejszenie liczby potrzeby kalibrować lub uczenie modelu przy użyciu funkcji. Funkcje wybrane do nauczenia modelu ze sobą matematycznie rzecz biorąc, są minimalny zbiór zmienne niezależne, które wyjaśniają wzorce w danych, a następnie pomyślnie przewidywania wyników.

Inżynieryjne i wybór funkcji jest częścią większego procesu, które zwykle obejmuje cztery kroki:

* Zbieranie danych
* Rozszerzenie danych
* Konstruowania modelu
* Przetwarzanie końcowe

Inżynieryjne i wybór tworzą kroku rozszerzenie danych usługi machine learning. Trzy aspekty tego procesu można wyróżnić dla naszych celów:

* **Przetwarzanie wstępne danych**: ten proces próbuje upewnij się, że zebranych danych jest czysty i spójne. Zawiera zadania, takie jak integrowanie wiele zestawów danych, obsługa brakujące dane, obsługa niespójne dane i konwertowanie typów danych.
* **Inżynieria**: ten proces próbuje utworzyć dodatkowe funkcje odpowiednie na podstawie istniejących funkcji pierwotnych danych oraz zwiększenie predykcyjnej zasilania Algorytm uczenia.
* **Wybór funkcji**: tego procesu wybiera klucza podzbiór oryginalnego funkcji danych, aby zmniejszyć wymiary problemu szkolenia.

W tym temacie opisuje tylko inżynieryjne funkcji i funkcji wyboru aspektów procesu rozszerzenia danych. Aby uzyskać więcej informacji na etapie wstępnego przetwarzania danych, zobacz [wstępne przetworzenie danych w usłudze Azure Machine Learning Studio](https://azure.microsoft.com/documentation/videos/preprocessing-data-in-azure-ml-studio/).

## <a name="creating-features-from-your-data--feature-engineering"></a>Tworzenie funkcji z danych--Inżynieria
Dane szkoleniowe składa się z macierzy składa się z przykładami (rekordy lub obserwacji przechowywane w wierszach), z których każda ma zestaw funkcji (zmienne lub pól przechowywane w kolumnach). Oczekiwano funkcji określony w projekcie doświadczenia charakteryzujących wzorce w danych. Mimo że wiele pól danych pierwotnych mogą być bezpośrednio uwzględnione w wybranej funkcji używany do nauczenia modelu, dodatkowe funkcje odtworzone często muszą zostać utworzone na podstawie funkcji w danych pierwotnych do generowania rozszerzone szkoleniowy zestaw danych.

Jakiego rodzaju funkcje należy utworzyć w celu ulepszenia zestawu danych podczas uczenia modelu? Odtworzone funkcji, które zwiększają szkolenia dostarczają informacji lepiej odróżniającą wzorce w danych. Oczekuje nowe funkcje, które znajdują się dodatkowe informacje, które nie jest wyraźnie przechwycona lub łatwo widoczna w zestaw oryginalnej lub istniejących funkcji, ale proces ten jest coś grafiki. Decyzje dźwięku i produktywności często wymagają doświadczenia z niektórych domen.

Począwszy od usługi Azure Machine Learning, najłatwiej konkretnie ujmij ten proces, za pomocą przykłady podane w usłudze Machine Learning Studio. Poniżej przedstawiono dwa przykłady:

* Przykład regresji ([prognozowanie liczby dzierżawy roweru](http://gallery.cortanaintelligence.com/Experiment/Regression-Demand-estimation-4)) w nadzorowanym eksperymentu, gdy wiadomo, że wartości docelowej
* Używając przykład klasyfikacji wyszukiwania tekstu [Tworzenie skrótu funkcji][feature-hashing]

### <a name="example-1-adding-temporal-features-for-a-regression-model"></a>Przykład 1: Dodawanie funkcji danych czasowych dla modelu regresji
Aby zademonstrować sposób opracowywać funkcje zadania regresji, Użyjmy eksperymentu "żądanie Prognozowanie rowerów" w usłudze Azure Machine Learning Studio. Celem tego eksperymentu jest do prognozowania popytu na rowerów, oznacza to, że liczba roweru dzierżawy w określonym miesiącu, dzień lub godzinę. Zestaw danych **zestawu danych UCI wynajem roweru** służy jako nieprzetworzone dane wejściowe.

Ten zestaw danych jest oparty na prawdziwe dane z firmy Bikeshare kapitału, która obsługuje sieci wynajem roweru w stanie Waszyngton DC w Stanach Zjednoczonych. Zestaw danych reprezentuje liczbę roweru dzierżawy w ciągu określonej godziny, dnia, 2011 2012 i zawiera 17379 wierszy i kolumn 17. Zestaw funkcji raw zawiera pogodą (temperatury, wilgotności, szybkość knie) i typ dzień (dni wolnych lub dzień tygodnia). W polu do prognozowania jest **cnt**, liczba reprezentująca dzierżawy roweru w ciągu godziny określonych i który od 1 do 977.

Do utworzenia skuteczne funkcje dane szkoleniowe, cztery modele regresji są tworzone za pomocą tego samego algorytmu, ale z cztery zestawy danych różnych szkolenia. Cztery zestawy danych reprezentują tego samego pierwotnych danych wejściowych, ale z coraz więcej funkcji ustawiona. Te funkcje są podzielone na kategorie cztery:

1. A = pogody + świątecznych dzień tygodnia + weekendowe funkcje przewidywane dzień
2. B = liczba rowerów, które zostały dzierżawione w każdym z ostatnich 12 godzin
3. C = Liczba rowerów, które zostały dzierżawione w każdym z ostatnich 12 dni na tę samą godzinę
4. D = liczba rowerów, które zostały dzierżawione w każdym z poprzednich 12 tygodni na tę samą godzinę i tego samego dnia

Oprócz A zestaw funkcji, który już istnieje w oryginalnych danych pierwotnych, trzy inne zestawy funkcji są tworzone za pomocą funkcji inżynierii procesu. Zestaw funkcji przechwytywania B ostatnie żądanie dla rowerów. Skonfigurować funkcji przechwytywania C popytu na rowerów o określonej godzinie. Funkcja ustawiona D przechwytywania żądanie dla rowerów w szczególności godziny i dnia tygodnia. Każdy z czterech zestawów danych szkoleniowych obejmuje zestawy funkcji A, A + B + C, A + B i A + B + C + D odpowiednio.

W eksperymencie usługi Azure Machine Learning te cztery zestawy danych szkoleniowych są tworzone za pomocą czterech oddziałów z zestawu wstępnie przetworzonych danych wejściowych. Z wyjątkiem pierwszej gałęzi, każdy z tych gałęzi zawiera [wykonanie skryptu języka R] [ execute-r-script] odpowiednio wykonane i dołączone do modułu, w którym zestaw pochodnych funkcji (funkcja ustawia B, C i D) zaimportowany zestaw danych. Na poniższym rysunku pokazano skrypt języka R, użyty do utworzenia zestawu funkcji B w drugim gałęzi po lewej stronie.

![Utwórz zestaw funkcji](./media/machine-learning-feature-selection-and-engineering/addFeature-Rscripts.png)

W poniższej tabeli przedstawiono porównanie wydajności wyników czterech modeli. Najlepsze wyniki są wyświetlane przez funkcje A + B + C. Należy pamiętać, że zmniejsza częstotliwość błędów zestawy dodatkowych funkcji została uwzględniona w danych szkoleniowych. Zweryfikuje naszych założenie, że zestawy funkcji B i C zapewniają dodatkowe istotne informacje o zadaniu regresji. Dodawanie zestawu funkcji D nie wydaje się zapewnienie każde dodatkowe zmniejszenie współczynnik błędów.

![Porównaj wyniki wydajności](./media/machine-learning-feature-selection-and-engineering/result1.png)

### <a name="example2"></a>Przykład 2: Tworzenie funkcji wyszukiwania tekstu
Funkcja engineering jest powszechnie stosowane w zadania związane z wyszukiwania tekstu, takich jak analiza dokumentu klasyfikacji i wskaźniki nastrojów klientów. Na przykład można klasyfikować dokumenty na kilka kategorii, typowe założeń jest słów ani fraz zawarte w jednej kategorii dokumentu jest mniej prawdopodobne w innej kategorii dokumentu. Innymi słowy częstotliwość dystrybucji wyraz lub frazę jest w stanie określić innego dokumentu kategorii. W aplikacjach wyszukiwania tekstu funkcja inżynierii procesu jest potrzebne do utworzenia funkcje dotyczące częstotliwości wyraz lub frazę, ponieważ pojedynczych zawartość tekstową zwykle służą jako danych wejściowych.

Do wykonania tego zadania, nazywany technika *Tworzenie skrótu funkcji* jest stosowany do wydajnie Włączanie funkcji dowolnego tekstu do indeksów. Zamiast kojarzenie każdej funkcji tekst (słów ani fraz) do konkretnego indeksu, to funkcje — metoda przez zastosowanie funkcji skrótu do funkcji i za pomocą wartości skrótu jako indeksy bezpośrednio.

W usłudze Azure Machine Learning [Tworzenie skrótu funkcji] [ feature-hashing] moduł, który tworzy te funkcje wyraz lub frazę. Na poniższej ilustracji przedstawiono przykład za pomocą tego modułu. Wejściowy zestaw danych zawiera dwie kolumny: Klasyfikacja książki z zakresu od 1 do 5 i rzeczywiste Przejrzyj zawartość. Celem tego [Tworzenie skrótu funkcji] [ feature-hashing] modułu jest pobrać nowe funkcje, które częstotliwość występowania odpowiednich słów ani fraz w ramach przeglądu wybranej książki. Aby użyć tego modułu, należy wykonać następujące czynności:

1. Wybierz kolumnę, która zawiera tekst wejściowy (**Col2** w tym przykładzie).
2. Ustaw *mieszania bitsize* 8, co oznacza 2 ^ 8 = 256 funkcje są tworzone. Wyraz lub frazę w tekście jest następnie mieszany do 256 indeksów. Parametr *mieszania bitsize* może się wahać od 1 do 31. Jeśli parametr jest ustawiona na większą liczbę, jest mniej prawdopodobne można przemieszać do tego samego indeksu słów ani fraz.
3. Ustaw dla parametru *N-gramów* 2. Częstotliwość występowania unigrams (funkcja dla każdego pojedynczego wyrazu) i bigrams (funkcja dla każdej pary słów sąsiadujące) to pobiera z teksu wejściowego. Parametr *N-gramów* w zakresie od 0 do 10, który wskazuje maksymalną liczbę kolejnych słowa do uwzględnienia w funkcji.  

![Funkcja wyznaczania wartości skrótu modułu](./media/machine-learning-feature-selection-and-engineering/feature-Hashing1.png)

Na poniższej ilustracji przedstawiono wygląd te nowe funkcje.

![Przykład skrótu funkcji](./media/machine-learning-feature-selection-and-engineering/feature-Hashing2.png)

## <a name="filtering-features-from-your-data--feature-selection"></a>Funkcje filtrowania danych — Wybieranie funkcji
*Wybór funkcji* jest procesem, który jest powszechnie stosowany do konstrukcji zestawów danych szkoleniowych modelowania predykcyjnego zadań, takich jak zadania klasyfikacji lub regresji. Celem jest wybierać podzestaw funkcji z oryginalnego zestawu danych pozwala ona zmniejszyć jego wymiary za pomocą minimalny zestaw funkcji do reprezentowania maksymalną ilość wariancji w danych. Ten zestaw funkcji zawiera tylko funkcje, które mają zostać uwzględnione do uczenia modelu. Wybór funkcji służy dwa główne cele:

* Wybór funkcji często zwiększa dokładność klasyfikacji przez wyeliminowanie nie ma znaczenia, nadmiarowe lub ściśle powiązane funkcje.
* Wybór funkcji zmniejsza liczbę funkcji, dzięki czemu większą wydajność procesu uczenia modelu. Jest to szczególnie ważne w przypadku uczących, które są kosztowne do uczenia, takich jak obsługa wektor maszyny.

Chociaż wybór funkcji ma na celu ograniczenia liczby funkcji w zestawie danych używany do nauczenia modelu, jego jest zwykle nieokreślonych przez określenie *redukcji wymiary.* Metody wyboru funkcji Wyodrębnij podzbioru cech oryginalnych danych bez konieczności ich zmieniania.  Wymiary metod redukcji stosować odtworzone funkcje, które można przekształcić funkcji oryginalnego i w związku z tym ich modyfikować. Przykładami metod redukcji wymiary analizy głównych składników, analiza canonical korelacji i dekompozycji pojedynczej wartości.

Jedną z powszechnie stosowanych kategorii metody wyboru funkcji w kontekście nadzorowany jest wybór funkcji na podstawie filtru. Wyniku obliczenia korelacji między każdej funkcji i atrybut target, te metody się statystyczne miarę w celu Przypisz wynik do każdej funkcji. Funkcje są następnie uporządkowane według wynik, w którym można ustawić próg utrzymywanie lub wyeliminowanie określonych funkcji. Przykładami miar statystyczne w tych metod korelacji wariancji x, wzajemne informacji i test chi kwadrat.

Azure Machine Learning Studio udostępnia moduły wybór funkcji. Jak pokazano na poniższej ilustracji, te moduły obejmują [na podstawie filtru wybór funkcji] [ filter-based-feature-selection] i [analiza liniowa Discriminant Fishera][fisher-linear-discriminant-analysis].

![Przykład wybór funkcji](./media/machine-learning-feature-selection-and-engineering/feature-Selection.png)

Na przykład użyć [na podstawie filtru wybór funkcji] [ filter-based-feature-selection] moduł przykład wyszukiwania tekstu opisane wcześniej. Domyślnym wariantem do tworzenia modelu regresji po utworzeniu zestaw funkcji 256 za pośrednictwem [Tworzenie skrótu funkcji] [ feature-hashing] modułu, a zmienna odpowiedzi jest **Col1** i reprezentuje książki przeglądu klasyfikacji z zakresu od 1 do 5. Ustaw **funkcji metody oceniania** do **korelacji wariancji x**, **kolumny docelowej** do **Col1**, i **żądaną liczbę Funkcje** do **50**. Moduł [na podstawie filtru wybór funkcji] [ filter-based-feature-selection] spowoduje utworzenie zestawu danych zawierającego 50 funkcji z atrybut target **Col1**. Na poniższej ilustracji przedstawiono przepływ tego eksperymentu i parametry wejściowe.

![Przykład wybór funkcji](./media/machine-learning-feature-selection-and-engineering/feature-Selection1.png)

Na poniższej ilustracji przedstawiono wynikowych zestawów danych. Każdej funkcji są oceniane na podstawie na korelacji wariancji x między sobą i atrybut target **Col1**. Funkcje z najwyższym wyniki są zachowywane.

![Zestawy danych funkcję Filtr na podstawie zaznaczenia](./media/machine-learning-feature-selection-and-engineering/feature-Selection2.png)

Na poniższej ilustracji przedstawiono odpowiednie wyniki wybranych funkcji.

![Wyniki wybranej funkcji](./media/machine-learning-feature-selection-and-engineering/feature-Selection3.png)

Stosując to [na podstawie filtru wybór funkcji] [ filter-based-feature-selection] modułu, 50 poza 256 funkcje są wybrane, ponieważ mają one większość funkcji skorelowane z Zmienna docelowa **Col1**oparte na metodzie oceniania **korelacji wariancji x**.

## <a name="conclusion"></a>Podsumowanie
Funkcja inżynieryjne i wybór funkcji są należy wykonać dwie czynności wykonywanych w celu przygotowania danych szkoleniowych, podczas tworzenia modelu uczenia maszynowego. Zwykle engineering funkcji zostanie zastosowana jako pierwsza, aby wygenerować dodatkowe funkcje, a następnie na etapie wyboru funkcji jest wykonywana w celu wyeliminowania nie ma znaczenia, nadmiarowe lub dużej skorelowane funkcji.

Nie zawsze jest zawsze do wykonywania funkcji engineering lub funkcji wyboru cech. Określa, czy jest potrzebny zależy od tego, ma lub zbierać dane, algorytmu, który można wybrać i celem eksperymentu.

<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[feature-hashing]: https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/
[filter-based-feature-selection]: https://msdn.microsoft.com/library/azure/918b356b-045c-412b-aa12-94a1d2dad90f/
[fisher-linear-discriminant-analysis]: https://msdn.microsoft.com/library/azure/dcaab0b2-59ca-4bec-bb66-79fd23540080/
