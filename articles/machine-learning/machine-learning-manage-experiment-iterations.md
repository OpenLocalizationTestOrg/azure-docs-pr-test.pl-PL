---
title: "aaaManage eksperymentu iteracji w usłudze Machine Learning Studio | Dokumentacja firmy Microsoft"
description: "Jak toomanage eksperymentu iteracji w usłudze Azure Machine Learning Studio"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 6a53530f-20d5-40ae-9b49-7b499ccb44b7
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: bd30c048ce063811b1b2de8ce6d71e99ba975713
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-experiment-iterations-in-azure-machine-learning-studio"></a>Zarządzanie iteracjami eksperymentów w usłudze Azure Machine Learning Studio
Podczas modyfikowania hello opracowywania modelu analizy predykcyjnej jest procesem iteracyjnym — różne funkcje i parametry eksperymentu, wyniki stają się zbieżne aż do uzyskania czy masz wyuczonego, skutecznego modelu. Proces toothis klucza jest hello śledzenia różnych iteracje eksperymentu parametrów i konfiguracji.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Możesz przejrzeć poprzedniej działa z eksperymentów w dowolnym momencie w kolejności toochallenge, ponownie i ostatecznie potwierdzić lub uściślić założenia poprzedniej. Po uruchomieniu eksperymentu Machine Learning Studio zawiera historię hello Uruchom, w tym zestaw danych, modułu, port połączenia i parametry. Ta historia przechwytuje także wyniki, informacje środowiska uruchomieniowego start i czasy zatrzymania, komunikaty dziennika i stan wykonania. Można przyjrzeć się wstecz żadnego z tych działa z dowolnego czasu tooreview hello chronologii eksperymentu, a wyniki pośrednie. Nawet służy poprzedniego uruchomienia toolaunch Twojego eksperymentu w nowej fazy zapytania i odnajdywania na Twoje ścieżki toocreating proste, złożonych lub nawet zespół modelowania rozwiązania.

> [!NOTE]
> Po wyświetleniu poprzedniego uruchomienia eksperymentu tej wersji eksperymentu hello jest zablokowany i nie można edytować. Można jednak zapisać kopię, klikając **SAVE AS** i podając nazwę hello kopiowania. Usługa Machine Learning Studio otwiera nową kopię hello, który można edytować i uruchomić. Ta kopia eksperymentu jest dostępna w hello **EKSPERYMENTY** listy oraz wszystkich innych eksperymentów.
> 
> 

## <a name="viewing-hello-prior-run"></a>Wyświetlanie hello poprzedniego uruchomienia
Masz otwarty eksperymentu uruchamianego co najmniej raz, można wyświetlić hello poprzedzających Uruchom hello eksperyment, klikając **uprzedniego uruchomienia** w okienku properties hello.

Załóżmy na przykład, tworzenie eksperymentu, a jednocześnie wersje 11:23 11:42 i 11:55. Otwórz hello ostatnim uruchomieniu eksperymentu hello (11:55) i kliknięcie **uprzedniego uruchomienia**, uruchomiono na 11:42 wersji hello jest otwarty.

## <a name="viewing-hello-run-history"></a>Wyświetlanie hello Uruchom historii
Można wyświetlić wszystkich poprzednich uruchomień hello eksperyment, klikając **Wyświetl historię uruchamiania** w eksperymencie otwarte.

Na przykład załóżmy tworzenie eksperymentów z hello [regresji liniowej] [ linear-regression] modułu, a ma tooobserve hello wpływu zmiany wartości hello **tempo uczenia** na wyniki eksperymentu. Możesz uruchomić eksperyment hello wiele razy z różnych wartości tego parametru, w następujący sposób:

| Wartość współczynnika Learning | Czas rozpoczęcia wykonywania |
| --- | --- |
| 0.1 |2014-9-11 4:18:58 pm |
| 0.2 |2014-9-11:24:33 PM. |
| 0.4 |2014-9-11 4:28:36 pm |
| 0.5 |2014-9-11 4:33:31 pm |

Jeśli klikniesz przycisk **WYŚWIETL HISTORIĘ URUCHAMIANIA**, wyświetlić listę wszystkich tych działa:

![Przykład Historia uruchomień][runhistory]

Kliknij dowolny z tych tooview uruchamia migawkę hello eksperymentu w czasie hello, który został on uruchomiony. Witaj konfiguracji, wartości parametrów, komentarze i wyniki są wszystkie zachowanego toogive możesz zarejestrować całe uruchamiane eksperymentu.

> [!TIP]
> toodocument Twojego iteracje eksperymentu hello można zmodyfikować tytuł hello każdym uruchomieniu, można zaktualizować hello **Podsumowanie** hello eksperymentu w okienku properties hello oraz można dodać lub zaktualizować komentarze dotyczące poszczególnych modułów toorecord zmiany. komentarze tytuł, podsumowanie i moduł Hello są zapisywane przy każdym uruchomieniu hello eksperymentu.
> 
> 

Lista Hello eksperymenty w hello **EKSPERYMENTY** karty w usłudze Machine Learning Studio zawsze wyświetla hello najnowszą wersję eksperymentu. Po otwarciu poprzedniego uruchomienia eksperymentu hello (przy użyciu **uprzedniego uruchomienia** lub **WYŚWIETL HISTORIĘ URUCHAMIANIA**), można powrócić toohello wersję roboczą, klikając **WYŚWIETL HISTORIĘ URUCHAMIANIA** i wybierając polecenie Witaj iteracji, które ma **stanu** z **edytowalna**.

## <a name="iterating-on-a-previous-run"></a>Iteracja na poprzedniego działania
Po kliknięciu **uprzedniego uruchomienia** lub **WYŚWIETL HISTORIĘ URUCHAMIANIA** i otwórz poprzedniego uruchomienia, Zakończono eksperymentu można wyświetlić w trybie tylko do odczytu.

Jeśli chcesz toobegin iterację eksperymentu począwszy sposób hello skonfigurowanych dla poprzedniego uruchomienia, można to zrobić otwierania hello Uruchom i klikając przycisk **SAVE AS**. Spowoduje to utworzenie nowy eksperyment z nowy tytuł pusty Historia uruchomień i wszystkie składniki hello i wartości parametrów hello poprzedniego uruchomienia. Ten nowy eksperyment ma na liście hello **EXPERIMENTS** karcie Strona główna hello Machine Learning Studio, a można modyfikować i ją uruchomić, inicjowanie nowy Uruchom historii dla tej iteracji eksperymentu. 

Załóżmy na przykład uruchomienie historii wyświetlone w poprzedniej sekcji hello hello eksperymentu. Ma tooobserve co się stanie, gdy wartość hello **tempo uczenia** too0.4 parametr i spróbuj różnych wartości hello **liczba epok szkolenia** parametru.

1. Kliknij przycisk **WYŚWIETL HISTORIĘ URUCHAMIANIA** , a następnie otwórz hello iterację eksperymentu hello, uruchomionego godzinie 4:28:36 (w którym można ustawić too0.4 wartość parametru hello).
2. Kliknij przycisk **SAVE AS**.
3. Wprowadź nowy tytuł, a następnie kliknij przycisk hello **OK** znacznik wyboru. Utworzono nową kopię hello eksperymentu.
4. Modyfikowanie hello **liczba epok szkolenia** parametru.
5. Kliknij przycisk **Uruchom**.

Można teraz kontynuować toomodify i będzie działać ta wersja eksperymentu, tworzenie nowych toorecord Historia uruchomień swoją pracę.

<!-- Images -->
[runhistory]:./media/machine-learning-manage-experiment-iterations/viewrunhistory.jpg


<!-- Module References -->
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/
