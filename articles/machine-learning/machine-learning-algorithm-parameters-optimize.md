---
title: "aaaOptimize algorytmy w usłudze Azure Machine Learning | Dokumentacja firmy Microsoft"
description: "W tym artykule wyjaśniono, jak parametr optymalne hello toochoose ustawiony dla algorytmu w usłudze Azure Machine Learning."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6717e30e-b8d8-4cc1-ad0b-1d4727928d32
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: fbf2f71abdbce19483fb048d67a39cbb368a928e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="choose-parameters-toooptimize-your-algorithms-in-azure-machine-learning"></a>Wybierz parametry toooptimize algorytmy w usłudze Azure Machine Learning
W tym temacie opisano, jak ustawić hyperparameter prawo hello toochoose dla algorytmu w usłudze Azure Machine Learning. Większość algorytmów uczenia maszynowego ma tooset parametrów. Podczas uczenia modelu, należy tooprovide wartości dla tych parametrów. Witaj skuteczności hello uczonego modelu zależy od parametrów modelu hello, które można wybrać. Witaj proces odnajdywania hello optymalne zestaw parametrów jest nazywany *modelu zaznaczenia*.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Istnieją różne sposoby toodo modelu zaznaczenia. W uczeniu maszynowym, krzyżowe sprawdzanie poprawności jest jedną z metod hello najczęściej używane do wyboru modelu i jest hello domyślnego modelu zaznaczenia mechanizmu w usłudze Azure Machine Learning. Ponieważ uczenia maszynowego Azure obsługuje R i Python, zawsze można zaimplementować własne mechanizmy wybór modelu przy użyciu R lub Python.

Istnieją cztery kroki w procesie hello wyszukiwanie hello najlepsze zestaw parametrów:

1. **Zdefiniuj hello parametr miejsca**: dla algorytmu hello najpierw zdecyduj, hello parametru dokładne wartości, które mają tooconsider.
2. **Definiowanie ustawień krzyżowego sprawdzania poprawności hello**: zdecydować, jak toochoose krzyżowego sprawdzania poprawności złożeń hello zestawu danych.
3. **Zdefiniuj Metryka hello**: Zdecyduj, jakie metryki toouse określania hello najlepsze zestaw parametrów, takich jak dokładność, średniej głównego kwadrat błąd, dokładność, odwołania lub wynik f.
4. **Uczenie, ocenę i porównywania**: dla każdej kombinacji unikatowe wartości parametrów hello krzyżowego sprawdzania poprawności jest przeprowadzane przez i oparta na zdefiniowaniu metryki błąd hello. Po oceny i porównania możesz wybrać hello najlepiej wykonywania modelu.

następujące obraz powitania przedstawiono pokazuje, jak można to osiągnąć w usłudze Azure Machine Learning.

![Znajdź hello najlepsze zestaw parametrów](./media/machine-learning-algorithm-parameters-optimize/fig1.png)

## <a name="define-hello-parameter-space"></a>Zdefiniuj hello parametr miejsca
Można określić parametru hello na kroku inicjowania hello modelu. Witaj parametru okienku wszystkich algorytmów uczenia maszynowego w dwóch trybach trainer: *pojedynczy parametr* i *zakres parametru*. Wybierz tryb zakres parametru. W trybie parametru zakresu można wprowadzić wiele wartości dla każdego parametru. W polu tekstowym hello można wprowadzić wartości rozdzielanych przecinkami.

![Drzewo decyzyjne boosted dwuklasowych, jeden parametr](./media/machine-learning-algorithm-parameters-optimize/fig2.png)

 Alternatywnie można zdefiniować hello maksymalne i minimalne punktów hello siatki i hello łączna liczba punktów toobe wygenerowane z **Użyj konstruktora zakresu**. Domyślnie program hello wartości parametrów są generowane na skali liniowej. Jeśli jednak **skali logarytmicznej** zaznaczono wartości hello są generowane w skali logarytmicznej hello (stosunek hello sąsiadujących punktów hello jest stałe zamiast ich różnica). Dla parametrów liczba całkowita można zdefiniować zakres przy użyciu łącznika. Na przykład, "1-10" oznacza, że wszystkie liczby całkowite z przedziału od 1 do 10 (włącznie) formularza hello zestaw parametrów. Tryb mieszany jest również obsługiwany. Na przykład Witaj zestaw parametrów "1-10, 20, 50" obejmuje liczb całkowitych 1-10, 20 do 50.

![Drzewo decyzyjne boosted dwuklasowych, parametr zakresu](./media/machine-learning-algorithm-parameters-optimize/fig3.png)

## <a name="define-cross-validation-folds"></a>Zdefiniuj złożeń krzyżowego sprawdzania poprawności
Witaj [partycja i próbka] [ partition-and-sample] moduł może być używane toorandomly Przypisz złożeń toohello danych. W hello po Przykładowa konfiguracja modułu hello możemy zdefiniować pięć złożeń i losowo przypisać złożenia liczba wystąpień próbki toohello.

![Partycja i próbka](./media/machine-learning-algorithm-parameters-optimize/fig4.png)

## <a name="define-hello-metric"></a>Zdefiniuj Metryka hello
Witaj [Hiperparametry modelu] [ tune-model-hyperparameters] modułu zapewnia obsługę empirycznie Wybieranie hello najlepsze zestawu parametrów dla podanego algorytmu i zestawu danych. Ponadto tooother informacji dotyczących szkoleń hello modelu hello **właściwości** okienko ten moduł zawiera metrykę hello określania hello najlepsze zestaw parametrów. Ma on dwa pola listy rozwijanej różnych algorytmów klasyfikacji i regresji, odpowiednio. Algorytm hello pod uwagę w przypadku algorytm klasyfikacji, metryka regresji hello jest ignorowany i na odwrót. W tym przykładzie określonych hello Metryka to **dokładność**.   

![Parametry odchylenia](./media/machine-learning-algorithm-parameters-optimize/fig5.png)

## <a name="train-evaluate-and-compare"></a>Uczenie, ocenę i porównywania
Witaj sam [Hiperparametry modelu] [ tune-model-hyperparameters] modułu przygotowuje wszystkie modele hello, które odpowiadają toohello zestaw parametrów, ocenia różnych metryk, a następnie tworzy najlepiej uczonego modelu hello oparte na powitania metryki, którą wybierzesz. Ten moduł ma dwóch parametrów wejściowych obowiązkowe:

* Uczeń nieprzeszkolonych Hello
* Witaj w zestawie danych

Moduł Hello ma również zestaw opcjonalne danych wejściowych. Zestaw danych hello Uzyskuj dostęp do złożenia informacji toohello obowiązkowe dataset w danych wejściowych. Jeśli hello dataset nie przypisano żadnych informacji złożenia, 10-krotnych krzyżowego sprawdzania poprawności automatycznie jest wykonywana domyślnie. Przypisania złożenia hello nie została wykonana, sprawdzanie poprawności zestawu danych znajduje się na powitania opcjonalny zestaw danych portu wybrany jest tryb train-test i hello pierwszego zestawu danych jest używane tootrain hello modelu dla każdej kombinacji parametrów.

![Klasyfikator drzewa decyzyjnego boosted](./media/machine-learning-algorithm-parameters-optimize/fig6a.png)

Hello model następnie jest obliczane w zestawie hello sprawdzania poprawności danych. Hello lewym portem wyjściowym hello moduł przedstawia różne metryki jako funkcje wartości parametrów. Prawy port wyjściowy daje hello uczonego modelu, który odpowiada toohello modelu najlepiej zostanie wykonana zgodnie z toohello wybrana Metryka Hello (**dokładność** w takim przypadku).  

![Sprawdzanie poprawności zestawu danych](./media/machine-learning-algorithm-parameters-optimize/fig6b.png)

Widać hello parametrami wybierany przez wizualizacja hello port wyjściowy prawo. Ten model można oceniania zestawu testowego lub usługi sieci web operationalized po zapisaniu jako uczonego modelu.

<!-- Module References -->
[partition-and-sample]: https://msdn.microsoft.com/library/azure/a8726e34-1b3e-4515-b59a-3e4a475654b8/
[tune-model-hyperparameters]: https://msdn.microsoft.com/library/azure/038d91b6-c2f2-42a1-9215-1f2c20ed1b40/
