---
title: aaaExtend eksperymentu z R | Dokumentacja firmy Microsoft
description: "Jak tooextend hello funkcje usługi Azure Machine Learning Studio za pomocą języka hello R przy użyciu modułu wykonania skryptu języka R hello."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 2c038a45-ba4d-42ea-9a88-e67391ef8c0a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: 396489f26f367a744922af65e04f056c7afa1399
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="extend-your-experiment-with-r"></a>Rozszerzanie eksperymentu przy użyciu języka R
Można rozszerzyć funkcjonalność hello Azure Machine Learning Studio za pomocą języka hello R przy użyciu hello [wykonanie skryptu języka R] [ execute-r-script] modułu.

Ten moduł akceptuje wiele zestawów danych wejściowych i daje jednego zestawu danych jako dane wyjściowe. Skrypt języka R można wpisać w hello **skrypt języka R** parametru hello [wykonanie skryptu języka R] [ execute-r-script] modułu.

Każdy port wejściowy modułu hello dostęp przy użyciu kodu podobne toohello poniżej:

    dataset1 <- maml.mapInputPort(1)

## <a name="listing-all-currently-installed-packages"></a>Wyświetlanie listy wszystkich aktualnie zainstalowane pakiety
można zmienić Hello listę zainstalowanych pakietów. Lista obecnie zainstalowanych pakietów można znaleźć w [R pakiety obsługiwanych przez usługi Azure Machine Learning](https://msdn.microsoft.com/library/azure/mt741980.aspx).

Również Ci hello pełną, bieżącą listę zainstalowanych pakietów wprowadzając powitania po kodu na powitania [wykonanie skryptu języka R] [ execute-r-script] modułu:

    out <- data.frame(installed.packages(,,,fields="Description"))
    maml.mapOutputPort("out")

To wysyła listę hello portem wyjściowym toohello pakietów hello [wykonanie skryptu języka R] [ execute-r-script] modułu.
Pakiet hello tooview listy, takich jak połączyć moduł konwersji [przekonwertować tooCSV] [ convert-to-csv] toohello pozostawione dane wyjściowe hello [wykonanie skryptu języka R] [ execute-r-script]modułu, uruchom eksperyment hello, następnie kliknij przycisk dane wyjściowe hello hello konwersji moduł i zaznacz **Pobierz**. 

![Pobieranie danych wyjściowych modułu "Przekonwertować tooCSV"](./media/machine-learning-extend-your-experiment-with-r/download-package-list.png)


<!--
For convenience, here is hello [current full list with version numbers in Excel format](http://az754797.vo.msecnd.net/docs/RPackages.xlsx).
-->

## <a name="importing-packages"></a>Importowanie pakietów
Można importować pakiety, które nie są już zainstalowane za pomocą następującego polecenia w hello hello [wykonanie skryptu języka R] [ execute-r-script] modułu:

    install.packages("src/my_favorite_package.zip", lib = ".", repos = NULL, verbose = TRUE)
    success <- library("my_favorite_package", lib.loc = ".", logical.return = TRUE, verbose = TRUE)

gdzie hello `my_favorite_package.zip` plik zawiera pakiet.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[convert-to-csv]: https://msdn.microsoft.com/library/azure/faa6ba63-383c-4086-ba58-7abf26b85814/
