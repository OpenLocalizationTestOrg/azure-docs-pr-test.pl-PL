---
title: "Wybór aaaFeature w hello proces nauki danych Team | Dokumentacja firmy Microsoft"
description: "Wyjaśnia hello celem wybór funkcji i przykłady ich roli w procesie rozszerzenie danych hello uczenia maszynowego."
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
ms.openlocfilehash: 54af93c83e4cc6a3670b3ad62490e0f74082b4ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="feature-selection-in-hello-team-data-science-process-tdsp"></a>Wybór funkcji w hello zespołu danych nauki procesu (TDSP)
W tym artykule opisano hello celów wybór funkcji oraz przykłady swoją rolę w procesie rozszerzenie danych hello uczenia maszynowego. Przykłady te są pobierane z usługi Azure Machine Learning Studio. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Witaj, inżynieria i wybór funkcji ma jedną część hello zespołu danych nauki procesu (TDSP) opisane w [co to jest hello proces nauki danych zespołu?](data-science-process-overview.md). Funkcja inżynieryjne i wyboru są części hello **opracowywania funkcji** krok hello TDSP.

* **Inżynieria**: ten proces próbuje toocreate dodatkowe istotne cechy z hello istniejących funkcji nieprzetworzone dane hello i algorytm uczenia toohello predykcyjnej zasilania tooincrease.
* **Wybór funkcji**: tego procesu wybiera hello klucza podzbioru cech oryginalnych danych w wymiarach hello tooreduce próba hello szkolenia problemu.

Zwykle **Inżynieria** zostanie zastosowane pierwszy toogenerate funkcje dodatkowe, a następnie hello **funkcji wyboru** krokiem jest wykonywane tooeliminate nie ma znaczenia, nadmiarowe lub dużej skorelowane funkcje.

## <a name="filtering-features-from-your-data---feature-selection"></a>Funkcje filtrowania danych - wybór funkcji
Wybór funkcji jest procesem, powszechnie stosowany do tworzenia hello zestawów danych szkoleniowych modelowania predykcyjnego zadań, takich jak zadania klasyfikacji lub regresji. Celem Hello jest tooselect podzbiór funkcji hello z oryginalnego zestawu danych hello zmniejszających wymiary przy użyciu minimalny zestaw funkcji toorepresent hello maksymalną ilość wariancji w hello danych. Są to podzbiór funkcji, a następnie hello tylko toobe funkcje uwzględnione tootrain hello modelu. Wybór funkcji służy dwa główne cele.

* Po pierwsze wybór funkcji często zwiększa dokładność klasyfikacji przez wyeliminowanie nie ma znaczenia, nadmiarowe lub ściśle powiązane funkcje.
* Po drugie zmniejsza hello wiele funkcji, dzięki czemu większą wydajność procesu uczenia modelu. Jest to szczególnie ważne w przypadku uczących będących tootrain kosztowne, takich jak obsługa wektor maszyny.

Mimo że wybór funkcji wyszukiwania tooreduce hello liczbę funkcji hello zestawu danych używane tootrain hello modelu, nie jest zazwyczaj określonego tooby hello termin "wymiarach redukcji". Metody wyboru funkcji Wyodrębnij podzbiór funkcji oryginalnego hello danych bez konieczności ich zmieniania.  Wymiary metod redukcji stosować odtworzone funkcje, które można przekształcić funkcji oryginalnego hello i w związku z tym ich modyfikować. Przykładami metod redukcji wymiary analizy składnika podmiot zabezpieczeń, analiza canonical korelacji i pojedynczą wartość rozkładu.

Między innymi jedną z powszechnie stosowanych kategorii metody wyboru funkcji w kontekście nadzorowany jest nazywany "Wybór funkcji Filtr na podstawie". Wyniku obliczenia hello korelacja poszczególnych funkcji i hello atrybut target, te metody mają zastosowanie tooassign statystyczne miary funkcji tooeach wynik. Funkcje Hello następnie są uporządkowane według hello wynik, który może być używane toohelp zestaw hello próg utrzymywanie lub wyeliminowanie określonych funkcji. Przykładami hello miar statystyczne w tych metod korelacji osoby, wzajemne informacji i hello Chi kwadrat testu.

W usłudze Azure Machine Learning Studio istnieją modułów dla funkcji wyboru cech. Jak pokazano na następującej ilustracji hello, te moduły obejmują [na podstawie filtru wybór funkcji] [ filter-based-feature-selection] i [analiza liniowa Discriminant Fishera] [ fisher-linear-discriminant-analysis].

![Przykład wybór funkcji](./media/machine-learning-data-science-select-features/feature-Selection.png)

Należy wziąć pod uwagę, na przykład użycie hello hello [na podstawie filtru wybór funkcji] [ filter-based-feature-selection] modułu. Witaj w celu zapewnienia wygody, w dalszym ciągu toouse hello wyszukiwania przykład tekstu opisanych powyżej. Załóżmy, że chcemy toobuild modelu regresji po zestaw funkcji 256 są tworzone za pomocą hello [Tworzenie skrótu funkcji] [ feature-hashing] modułu i zmiennej odpowiedzi hello jest hello "Col1" i reprezentuje książkę Przejrzyj klasyfikacje z zakresu od 1 too5. Ustawiając "Funkcja oceniania metody" toobe "Wariancji x korelacji" hello "Kolumna docelowa" toobe "Col1" i too50 "Liczba żądanych funkcji" hello. Następnie moduł hello [na podstawie filtru wybór funkcji] [ filter-based-feature-selection] spowoduje utworzenie zestawu danych zawierającego 50 funkcji z hello atrybut target "Col1". Hello następujący rysunek przedstawia przepływ hello tego eksperymentu i hello parametrów wejściowych, które firma Microsoft opisane.

![Przykład wybór funkcji](./media/machine-learning-data-science-select-features/feature-Selection1.png)

Witaj poniższej ilustracji przedstawiono hello Wynikowy zestaw danych. Każdej funkcji są oceniane na podstawie na powitania wariancji x korelacja sam i hello atrybut target "Col1". Funkcje Hello z najwyższym wyniki są zachowywane.

![Przykład wybór funkcji](./media/machine-learning-data-science-select-features/feature-Selection2.png)

w hello następującej ilustracji przedstawiono Hello odpowiednie wyniki hello wybrane funkcje.

![Przykład wybór funkcji](./media/machine-learning-data-science-select-features/feature-Selection3.png)

Stosując to [na podstawie filtru wybór funkcji] [ filter-based-feature-selection] modułu, 50 poza 256 funkcje są wybrane, ponieważ mają one hello większość skorelowane funkcji z Zmienna docelowa hello "Col1" oparte na powitania oceniania Metoda "Wariancji x korelacji".

## <a name="conclusion"></a>Podsumowanie
Funkcja inżynieryjne i wybór funkcji są dwa najczęściej odtwarzane i wybranych funkcji zwiększyć wydajność hello hello szkolenia procesu, który próbuje tooextract hello najważniejsze informacje zawarte w danych hello. One również poprawić zasilania hello te modele tooclassify hello danych wejściowych dokładnie i wyniki toopredict odsetek więcej niezawodnie. Funkcja inżynieryjne i wyboru można także połączyć learning hello toomake więcej praktyce tractable. Robi to przez rozszerzanie i następnie zmniejszeniu liczby hello funkcje wymagane toocalibrate lub train model. Ze sobą matematycznie rzecz biorąc, model hello tootrain wybrane funkcje hello są minimalny zbiór zmienne niezależne, hello wzorce w danych hello wyjaśnienia, które następnie pomyślnie przewidywania wyników.

Należy pamiętać, że nie zawsze jest zawsze tooperform funkcji engineering lub funkcji wyboru cech. Określa, czy jest potrzebna, lub nie zależy od danych hello mają lub zbierane hello algorytmu, który mamy pobranie i hello cel hello eksperymentu.

<!-- Module References -->
[feature-hashing]: https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/
[filter-based-feature-selection]: https://msdn.microsoft.com/library/azure/918b356b-045c-412b-aa12-94a1d2dad90f/
[fisher-linear-discriminant-analysis]: https://msdn.microsoft.com/library/azure/dcaab0b2-59ca-4bec-bb66-79fd23540080/

