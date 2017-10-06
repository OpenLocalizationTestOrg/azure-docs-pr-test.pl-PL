---
title: "aaaDebug modelu w usłudze Azure Machine Learning | Dokumentacja firmy Microsoft"
description: "Jak błędy toodebug utworzonego przez Train Model i Score Model moduły w usłudze Azure Machine Learning."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 629dc45e-ac1e-4b7d-b120-08813dc448be
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bradsev;garye
ms.openlocfilehash: ee38ca8ce38d4fc7add5ba70c80ab9bb2ceaf1d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="debug-your-model-in-azure-machine-learning"></a>Debugowanie modelu w usłudze Azure Machine Learning

W tym artykule opisano potencjalnych przyczyn hello, dlaczego albo powitania po awarii dwóch węzłów może napotkać podczas uruchamiania modelu:

* Witaj [Train Model] [ train-model] moduł powoduje błąd 
* Witaj [Score Model] [ score-model] modułu tworzy niepoprawnych wyników 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="train-model-module-produces-an-error"></a>Train Model moduł powoduje błąd

![image1](./media/machine-learning-debug-models/train_model-1.png)

Witaj [Train Model] [ train-model] modułu oczekuje dwóch parametrów wejściowych:

1. Typ Hello modelu uczenia maszynowego z kolekcji hello modeli udostępniane przez usługi Azure Machine Learning.
2. Witaj dane szkoleniowe z określonej kolumny etykiety, który określa hello toopredict zmiennej (hello innych kolumn są zakłada, że funkcje toobe).

Ten moduł może utworzyć błędu w hello w następujących przypadkach:

1. Witaj etykiety kolumn została określona nieprawidłowo. Może to nastąpić, jeśli wybrano więcej niż jedną kolumnę jako hello etykiety lub wybrano nieprawidłowy indeks. Na przykład hello drugim przypadku będą miały zastosowania, jeśli indeks kolumny 30 jest używany z wejściowego zestawu danych, która zawiera tylko 25 kolumn.

2. Witaj zestawu danych nie zawiera żadnych kolumn funkcji. Na przykład jeśli hello wejściowy zestaw danych zawiera tylko jedną kolumnę, która jest oznaczona jako kolumna etykiety hello, nie byłoby żadnych funkcji, z którym modelem hello toobuild. W takim przypadku hello [Train Model] [ train-model] moduł powoduje błąd.

3. Hello wejściowy zestaw danych (funkcji lub etykiety) zawiera nieskończoności jako wartość.

## <a name="score-model-module-produces-incorrect-results"></a>Moduł score Model tworzy niepoprawnych wyników

![image2](./media/machine-learning-debug-models/train_test-2.png)

W typowej szkolenia/testowania eksperyment do uczenia nadzorowanego, hello [podziału danych] [ split] modułu hello oryginalnego zestawu danych jest podzielony na dwie części: jednej strony jest używane tootrain hello modelu i używany jednej strony tooscore jak wykonuje hello trenowanego modelu. uczonego modelu Hello jest używane tooscore hello dane testowe, po którym hello wyniki są obliczane toodetermine dokładność hello hello modelu.

Witaj [Score Model] [ score-model] moduł wymaga dwóch parametrów wejściowych:

1. Dane wyjściowe uczonego modelu hello [Train Model] [ train-model] modułu.
2. Oceniania zestawu danych, który różni się od zestawu danych hello używane tootrain hello modelu.

Możliwe, że nawet jeśli eksperymentu hello zakończy się powodzeniem, hello tego [Score Model] [ score-model] modułu tworzy niepoprawnych wyników. Kilka scenariuszy może spowodować to toohappen:

1. Jeśli hello określona etykieta jest podzielone na kategorie i model regresji jest uczony na powitania danych, nieprawidłowych danych wyjściowych może być realizowane przez hello [Score Model] [ score-model] modułu. Jest to spowodowane regresji wymaga zmiennej ciągłego odpowiedzi. W takim wypadku byłoby odpowiedniejsze toouse model klasyfikacji. 

2. Podobnie jeśli model klasyfikacji jest uczony w zestawie danych o zmiennoprzecinkową liczby w kolumnie etykiety hello, może dać niepożądane wyniki. Jest to spowodowane klasyfikacji wymaga zmiennej odrębny odpowiedzi, która zezwala tylko wartości zakresu za pośrednictwem skończona i zwykle nieco mały zestaw klas.

3. Jeśli hello oceniania zestawu danych nie zawiera wszystkich hello funkcji używanych tootrain hello modelu, hello [Score Model] [ score-model] powoduje błąd.

4. Jeśli wiersz w hello oceniania dataset zawiera brakujące wartości lub nieskończona wartość dla każdego z jego funkcji, hello [Score Model] [ score-model] nie utworzy odpowiedni wiersz toothat żadnych danych wyjściowych.

5. Witaj [Score Model] [ score-model] może tworzyć identyczne dane wyjściowe dla wszystkich wierszy hello oceniania zestawu danych. To może wystąpić, na przykład podczas próby klasyfikacji za pomocą lasów decyzji, jeśli minimalna liczba próbek na węzeł liścia hello jest wybierany toobe ponad hello liczba dostępnych przykłady szkolenia.

<!-- Module References -->
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/

