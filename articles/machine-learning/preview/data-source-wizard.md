---
title: "Kreator Azure Machine Learning źródła danych Azure | Dokumentacja firmy Microsoft"
description: "Wyjaśniono AML środowiska roboczego Kreatora źródła danych"
services: machine-learning
author: cforbe
ms.author: cforbe
manager: mwinkle
ms.reviewer: garyericson, jasonwhowell, mldocs
ms.service: machine-learning
ms.workload: data-services
ms.topic: article
ms.date: 09/07/2017
ms.openlocfilehash: ff0159facd693b83230c731eb7e76f0a9495fdf2
ms.sourcegitcommit: 68aec76e471d677fd9a6333dc60ed098d1072cfc
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/18/2017
---
# <a name="data-source-wizard"></a>Kreator źródła danych #

Kreator źródła danych jest szybki i łatwy sposób dostosowania zestawu danych do usługi Azure ML Workbench bez kodu. Jest, gdzie można również wybrać strategii próbki dla zestawu danych. 

## <a name="step-1-trigger-the-data-source-wizard"></a>Krok 1: Wyzwolenia Kreatora źródła danych ## 

Aby przenieść dane do projektu przy użyciu Kreatora źródła danych. Wybierz  **+**  znajdujący się obok pola wyszukiwania w widoku danych i wybierz polecenie Dodaj źródło danych. 

![Dodawanie źródła danych](media/data-source-wizard/add-data-source.png)

## <a name="step-2-select-where-data-is-stored"></a>Krok 2: Wybierz, w którym są przechowywane dane ##
Najpierw określ, jak dane są obecnie w. Może być przechowywany w pliku prostego lub katalog, plik parquet, pliku programu Excel lub bazy danych. Zobacz [obsługiwanych źródeł danych](data-prep-appendix2-supported-data-sources.md) Aby uzyskać więcej informacji.

![Krok 1](media/data-source-wizard/step1.png)

## <a name="step-3-select-data-file"></a>Krok 3: Wybierz plik danych ##
Dla pliku/katalogu Określ ścieżkę do pliku. Wybierz z listy rozwijanej lokalizacji danych — ścieżka do pliku lokalnego i magazynu obiektów Blob Azure. 

Określ ścieżkę, wpisując w lub klikając **Przeglądaj...** Aby wyszukać. Można przeglądać w poszukiwaniu katalogu lub co najmniej jeden plik.

Kliknij przycisk **Zakończ** zaakceptuj wartości domyślne dla pozostałych kroków lub następnie przejść do następnego kroku.


![Krok 4](media/data-source-wizard/step2.png)

## <a name="step-4-choose-file-parameters"></a>Krok 4: Wybierz plik parametrów ##

Kreator źródła danych automatycznie wykrywa plik typu, separatory i kodowania. Będą również wyświetlane przykład wygląd danych. Można również zmienić dowolne z tych parametrów ręcznie. 

![Krok 5](media/data-source-wizard/step3.png)

## <a name="step-5-set-data-types-for-columns"></a>Krok 5: Ustaw typy danych kolumn ##

Kreator źródła danych automatycznie wykrywa typy danych kolumn w zestawie danych. Chybień buforu, jednego, czy ma zostać wymuszone typu danych, należy ręcznie zmienić typ danych. **Przykładowe dane wyjściowe** kolumna zawiera przykłady wygląd danych.

![Krok 6](media/data-source-wizard/step4.png)

## <a name="step-6-choose-sampling-strategy-for-data"></a>Krok 6: Wybierz strategię pobierania próbek danych ##

Można określić co najmniej jeden strategie dla zestawu danych i wybierz jedną jako aktywnej strategii. Wartość domyślna to załadować 10000 pierwszych wierszy. W tym przykładzie można edytować, klikając **Edytuj** przycisku w pasku narzędzi lub Dodaj nowe strategii przez kliknięcie + nowy. Strategie, które aktualnie obsługują

-     Górny liczbę wierszy
-     Liczba wierszy
-     Losowe odsetek wierszy
-     Całego pliku

Można określić dowolną liczbę strategie, ale jest tylko jeden, który może być ustawiona jako aktywna podczas przygotowywania danych. Można ustawić jako aktywna, wybierając strategii każdej strategii i kliknij przycisk Ustaw jako aktywny w pasku narzędzi.

W zależności od tego, gdzie dane pochodzą z kilka strategii próbki może nie być obsługiwana. Aby uzyskać więcej informacji o próbkowaniu sekcji próbkowania [tego dokumentu](data-prep-user-guide.md) 

![Krok 6](media/data-source-wizard/step5.png)

## <a name="step-7-path-column-handling"></a>Krok 7: Obsługa kolumny ścieżki ##

Ścieżka pliku zawiera ważne dane, można dołączyć go jako pierwsza kolumna w zestawie danych. Powinien to być przydatne, jeśli są przywracanie w wielu plikach. W przeciwnym razie można nie ma.

![Krok 7](media/data-source-wizard/step6.png)

Po kliknięciu przycisku Zakończ, nowe źródło danych zostanie dodany do projektu. Możesz go znaleźć w ramach grupy źródeł danych w widoku danych lub jako plik .dsource w **widoku pliku**.
