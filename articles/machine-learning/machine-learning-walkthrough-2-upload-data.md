---
title: "Krok 2: Prześlij dane do eksperymentu uczenia maszynowego | Dokumentacja firmy Microsoft"
description: "Krok 2 hello opracowanie wskazówki rozwiązanie predykcyjne: przekazywanie przechowywanych danych publicznych do usługi Azure Machine Learning Studio."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 9f4bc52e-9919-4dea-90ea-5cf7cc506d85
ms.service: machine-learning
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 0ea21dcca2d0934ed06508560cf85cf31b48ce6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-2-upload-existing-data-into-an-azure-machine-learning-experiment"></a>Przewodnik, krok 2. Przekazywanie istniejących danych do eksperymentu usługi Azure Machine Learning
Jest to drugi etap wskazówki hello hello [tworzenie rozwiązania analizy predykcyjnej w usłudze Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)

1. [Tworzenie obszaru roboczego usługi Machine Learning](machine-learning-walkthrough-1-create-ml-workspace.md)
2. **Przekazywanie istniejących danych**
3. [Tworzenie nowego eksperymentu](machine-learning-walkthrough-3-create-new-experiment.md)
4. [Nauczanie i Ewaluacja modeli hello](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [Wdrażanie usługi sieci Web hello](machine-learning-walkthrough-5-publish-web-service.md)
6. [Witaj dostępu do usługi sieci Web](machine-learning-walkthrough-6-access-web-service.md)

- - -
toodevelop model predykcyjny dla oceny ryzyka kredytowego, potrzebujemy danych czy możemy użyć tootrain i przetestowanie hello modelu. W ramach tego przewodnika użyjemy hello "UCI Statlog (niemieckim dane środki) zestawu danych" hello UC Irvine Machine Learning repozytorium. Możesz go znaleźć tutaj:  
<a href="http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)">http://Archive.ICS.uci.edu/ml/DataSets/Statlog+(German+Credit+Data)</a>

Użyjemy hello plik o nazwie **german.data**. Pobierz plik tooyour lokalnym dysku twardym.  

Witaj **german.data** dataset zawiera wiersze 20 zmiennych dla 1000 ostatnich kandydatów do uznania. Te zmienne 20 reprezentują zestaw funkcji hello dataset (hello *wektor funkcji*), zapewniające cechy identyfikacyjne dla każdego zgłaszającego kredytowej. Dodatkowe kolumny w każdym wierszu reprezentuje kandydata hello ryzyka kredytowego obliczeniowej, z 700 kandydatami zidentyfikowane jako niskie ryzyko kredytowe i 300 jako wysokiego ryzyka.

Witaj UCI witryny sieci Web zawiera opis atrybutów hello hello wektor funkcji dla tych danych. W tym informacji finansowych, historii kredytów status zatrudnienia i informacje osobiste. Dla każdego zgłaszającego klasyfikacji binarnej został podany, wskazującą, czy są one niski lub wysoki ryzyka karty kredytowej. 

Użyjemy tego tootrain danych modelu analizy predykcyjnej. Gdy skończymy, nasz model powinny być możliwe tooaccept wektorem funkcji dla nowej osoby i prognozowania, czy użytkownik jest ryzyko kredytowe niski i wysoki.  

Oto interesujące dołączony. Witaj opis zestawu danych hello na powitania UCI witryny sieci Web uwagi kosztach jeśli mamy misclassify ryzyko kredytowe osoby.
Jeśli hello model przewiduje ryzyko kredytowe wysokiej osobie, która jest rzeczywiście niskie ryzyko kredytowe, hello model wprowadził błędną klasyfikację.
Ale odwrotnej błędną klasyfikację hello jest pięć razy bardziej kosztowne instytucji finansowej toohello: Jeśli hello model przewiduje niskie ryzyko kredytowe osoby, która jest rzeczywiście ryzyko kredytowe wysokiej.

Dlatego chcemy tootrain nasz model tak, aby koszt hello tego typu ostatnie błędu klasyfikacji pięć razy wyższa niż misclassifying hello inny sposób.
Jeden prosty sposób toodo to podczas uczenia modelu hello w naszym doświadczeniu jest duplikując (pięć razy) zapisów reprezentujących ktoś z ryzyko kredytowe wysoki. Następnie jeśli hello model klasyfikuje ktoś jako niskie ryzyko kredytowe, gdy są faktycznie wysokiego ryzyka, hello modelu nie tego samego błędu klasyfikacji pięć razy raz dla każdego duplikatu. To spowoduje zwiększenie kosztów hello tego błędu w wynikach szkolenia hello.


## <a name="convert-hello-dataset-format"></a>Konwertuj hello formacie zestawu danych
Witaj oryginalnego zestawu danych w formacie oddzielone puste. Usługa Machine Learning Studio działa lepiej z pliku wartości rozdzielanych przecinkami (CSV), więc będzie nie możemy przekonwertować zestawu danych hello zastępując spacje przecinkami.  

Istnieje wiele sposobów tooconvert tych danych. Jednym ze sposobów jest za pomocą następującego polecenia programu Windows PowerShell hello:   

    cat german.data | %{$_ -replace " ",","} | sc german.csv  

Innym sposobem jest za pomocą polecenia mniejszyć Unix hello:  

    sed 's/ /,/g' german.data > german.csv  

W obu przypadkach utworzono wersję przecinkami hello danych w pliku o nazwie **german.csv** który możemy użyć w naszym doświadczeniu.

## <a name="upload-hello-dataset-toomachine-learning-studio"></a>Przekaż hello dataset tooMachine Learning Studio
Po hello danych został przekonwertowany tooCSV format, potrzebujemy tooupload go do usługi Machine Learning Studio. 

1. Strona główna usługi Machine Learning Studio Otwórz hello ([https://studio.azureml.net](https://studio.azureml.net)). 

2. Kliknij hello menu ![Menu][1] w hello lewym górnym rogu okna hello, kliknij przycisk **usługi Azure Machine Learning**, wybierz pozycję **Studio**i zaloguj się.

3. Kliknij przycisk **+ nowy** u dołu okna hello hello.

4. Wybierz **zestawu danych**.

5. Wybierz **z pliku lokalnego**.

    ![Dodaj zestaw danych z pliku lokalnego][2]

6. W hello **przekazać nowy zestaw danych** okna dialogowego, kliknij przycisk **Przeglądaj** i Znajdź hello **german.csv** utworzony plik.

7. Wprowadź nazwę dla zestawu danych hello. W ramach tego przewodnika wywołać ją "Dane karty kredytowej niemiecki UCI".

8. Dla typu danych, wybierz **ogólnego pliku CSV bez nagłówka (. nh.csv)**.

9. Dodaj opis, jeśli chcesz.

10. Kliknij przycisk hello **OK** znacznik wyboru.  

    ![Przekaż hello zestawu danych][3]

Do modułu zestawu danych, które pomagają w eksperymencie operacji przekazywania danych hello.

Można zarządzać zestawów danych, klikając hello przesłaniu tooStudio **zestawów danych** toohello kartę pozostałych hello Studio okna.

![Zarządzanie zbiory danych][4]

Aby uzyskać więcej informacji o importowaniu inne typy danych do eksperymentu, zobacz [importowanie danych szkoleniowych w usłudze Azure Machine Learning Studio](machine-learning-data-science-import-data.md).

**Następnie: [Tworzenie nowego eksperymentu](machine-learning-walkthrough-3-create-new-experiment.md)**

[1]: media/machine-learning-walkthrough-2-upload-data/menu.png
[2]: media/machine-learning-walkthrough-2-upload-data/add-dataset.png
[3]: media/machine-learning-walkthrough-2-upload-data/upload-dataset.png
[4]: media/machine-learning-walkthrough-2-upload-data/dataset-list.png
