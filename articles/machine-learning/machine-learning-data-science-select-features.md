---
title: Funkcja zaznaczenia w procesie nauki danych Team | Dokumentacja firmy Microsoft
description: "Objaśnienie jego przeznaczenia wybór funkcji i przykłady ich roli w procesie rozszerzenie danych usługi machine learning."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 878541f5-1df8-4368-889a-ced6852aba47
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: zhangya;bradsev
ms.openlocfilehash: ab97ee8278be567ff46d9b0f762d3c5c6cafa412
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="feature-selection-in-the-team-data-science-process-tdsp"></a>Wybór funkcji w zespołowym przetwarzaniu danych dla celów naukowych
W tym artykule opisano na potrzeby funkcji wyboru oraz przykłady swoją rolę w procesie rozszerzenie danych usługi machine learning. Przykłady te są pobierane z usługi Azure Machine Learning Studio. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Inżynieryjne i wybór funkcji jest jedną z części z zespołu danych nauki procesu (TDSP) opisane w temacie [co to jest proces zespołu danych nauki?](data-science-process-overview.md). Funkcja inżynieryjne i wyboru są częściami **opracowywania funkcji** krok TDSP.

* **Inżynieria**: ten proces próbuje utworzyć dodatkowe istotne cechy z istniejących funkcji pierwotnych danych i zwiększyć predykcyjnej zasilania Algorytm uczenia.
* **Wybór funkcji**: tego procesu wybiera klucza podzbioru cech oryginalnych danych w celu zmniejszenia wymiarach problemu szkolenia.

Zwykle **Inżynieria** zostanie zastosowana jako pierwsza, aby wygenerować dodatkowe funkcje, a następnie **funkcji wyboru** kroku jest wykonywana w celu wyeliminowania nie ma znaczenia, nadmiarowe lub dużej skorelowane funkcji.

## <a name="filtering-features-from-your-data---feature-selection"></a>Funkcje filtrowania danych - wybór funkcji
Wybór funkcji jest procesem, powszechnie stosowany do tworzenia zbiorów danych szkoleniowych modelowania predykcyjnego zadań, takich jak zadania klasyfikacji lub regresji. Celem jest Wybierz podzbiór funkcji z oryginalnego zestawu danych zmniejszyć jego wymiary za pomocą minimalny zestaw funkcji do reprezentowania maksymalną ilość wariancji w danych. Następnie ten podzestaw funkcji są tylko funkcje do uwzględnienia do nauczenia modelu. Wybór funkcji służy dwa główne cele.

* Po pierwsze wybór funkcji często zwiększa dokładność klasyfikacji przez wyeliminowanie nie ma znaczenia, nadmiarowe lub ściśle powiązane funkcje.
* Po drugie zmniejsza liczbę funkcji, dzięki czemu większą wydajność procesu uczenia modelu. Jest to szczególnie ważne w przypadku uczących, które są kosztowne do uczenia, takich jak obsługa wektor maszyny.

Mimo że wybór funkcji wyszukiwania ograniczyć liczbę funkcji w zestawie danych używany do nauczenia modelu, jego jest nie zazwyczaj określone przez termin "wymiarach redukcji". Metody wyboru funkcji Wyodrębnij podzbioru cech oryginalnych danych bez konieczności ich zmieniania.  Wymiary metod redukcji stosować odtworzone funkcje, które można przekształcić funkcji oryginalnego i w związku z tym ich modyfikować. Przykładami metod redukcji wymiary analizy składnika podmiot zabezpieczeń, analiza canonical korelacji i pojedynczą wartość rozkładu.

Między innymi jedną z powszechnie stosowanych kategorii metody wyboru funkcji w kontekście nadzorowany jest nazywany "Wybór funkcji Filtr na podstawie". Wyniku obliczenia korelacji między każdej funkcji i atrybut target, te metody się statystyczne miarę w celu Przypisz wynik do każdej funkcji. Funkcje są następnie uporządkowane według wynik, który może służyć do ustawiać wartości progowej dla utrzymywanie lub wyeliminowanie określonych funkcji. Przykładami miar statystyczne w tych metod korelacji osoby, wzajemne informacji i test Chi kwadrat.

W usłudze Azure Machine Learning Studio istnieją modułów dla funkcji wyboru cech. Jak pokazano na poniższej ilustracji, te moduły obejmują [na podstawie filtru wybór funkcji] [ filter-based-feature-selection] i [analiza liniowa Discriminant Fishera][fisher-linear-discriminant-analysis].

![Przykład wybór funkcji](./media/machine-learning-data-science-select-features/feature-Selection.png)

Na przykład, rozważ użycie [na podstawie filtru wybór funkcji] [ filter-based-feature-selection] modułu. W celu zapewnienia wygody firma Microsoft nadal używać przykład wyszukiwania tekstu opisanych powyżej. Załóżmy chęć kompilacji modelu regresji po utworzeniu przez zestaw funkcji 256 [Tworzenie skrótu funkcji] [ feature-hashing] modułu, a zmienna odpowiedzi jest "Col1" reprezentuje książkę Przejrzyj klasyfikacje z zakresu od 1 do 5. Przez ustawienie "Funkcji oceniania metody" jako "Wariancji x korelacji", "kolumna docelowa" jako "Col1" i "Liczba żądanych funkcji" do 50. Następnie moduł [na podstawie filtru wybór funkcji] [ filter-based-feature-selection] spowoduje utworzenie zestawu danych zawierającego 50 funkcji z atrybut target "Col1". Na poniższej ilustracji przedstawiono przepływ tego eksperymentu i parametrów wejściowych, które firma Microsoft opisane.

![Przykład wybór funkcji](./media/machine-learning-data-science-select-features/feature-Selection1.png)

Na poniższej ilustracji przedstawiono Wynikowy zestaw danych. Każdej funkcji są oceniane na podstawie na korelacji wariancji x między sobą i atrybut target "Col1". Funkcje z najwyższym wyniki są zachowywane.

![Przykład wybór funkcji](./media/machine-learning-data-science-select-features/feature-Selection2.png)

Odpowiednie wyniki wybrane funkcje są wyświetlane na poniższej ilustracji.

![Przykład wybór funkcji](./media/machine-learning-data-science-select-features/feature-Selection3.png)

Stosując to [na podstawie filtru wybór funkcji] [ filter-based-feature-selection] modułu, 50 poza 256 funkcje są wybrane, ponieważ mają one funkcji najbardziej skorelowane z Zmienna docelowa "Col1", na podstawie wyników metody "Wariancji x korelacji".

## <a name="conclusion"></a>Podsumowanie
Funkcja inżynieryjne i wybór funkcji są dwa najczęściej odtwarzane i wybranych funkcji zwiększyć wydajność procesu szkolenia, który próbuje wyodrębnić informacje o kluczu zawarte w danych. Poprawiają również uprawnienia tych modeli dokładnie klasyfikowania danych wejściowych oraz do przewidywania wyników odsetek bardziej niezawodnie. Funkcja inżynieryjne i wyboru można także połączyć dokonanie więcej praktyce tractable learning. Robi to udoskonalanie, a następnie zmniejszenie liczby potrzeby kalibrować lub uczenie modelu przy użyciu funkcji. Funkcje wybrane do nauczenia modelu ze sobą matematycznie rzecz biorąc, są minimalny zbiór zmienne niezależne, które wyjaśniają wzorce w danych, a następnie pomyślnie przewidywania wyników.

Należy pamiętać, że nie zawsze musi przeprowadzić wybór funkcji engineering lub funkcji. Określa, czy jest potrzebna, lub nie zależy od tego, firma Microsoft ma lub zbierać dane, algorytmu, który mamy pobranie i celem eksperymentu.

<!-- Module References -->
[feature-hashing]: https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/
[filter-based-feature-selection]: https://msdn.microsoft.com/library/azure/918b356b-045c-412b-aa12-94a1d2dad90f/
[fisher-linear-discriminant-analysis]: https://msdn.microsoft.com/library/azure/dcaab0b2-59ca-4bec-bb66-79fd23540080/

