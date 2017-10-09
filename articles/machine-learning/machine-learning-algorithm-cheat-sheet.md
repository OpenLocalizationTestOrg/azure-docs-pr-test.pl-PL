---
title: "Arkusz ze wskazówkami dotyczącymi Algorytm uczenia aaaMachine | Dokumentacja firmy Microsoft"
description: "Maszynę do druku arkusz ze wskazówkami dotyczącymi Algorytm uczenia pomaga wybrać hello prawo algorytmu dla modelu predykcyjnego w usłudze Azure Machine Learning Studio."
keywords: "Algorytm przydatną ściągawkę, przydatną ściągawkę, algorytmu uczenia maszynowego"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: e1dc31ec-1acb-463f-ba77-de565d4ddf4d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: garye
ms.openlocfilehash: 2bedd77bfc65128a90c6128743016415dd8609d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="machine-learning-algorithm-cheat-sheet-for-microsoft-azure-machine-learning-studio"></a>Ściągawka dotycząca algorytmu uczenia maszynowego w usłudze Microsoft Azure Machine Learning Studio
Witaj **Microsoft Azure Machine Learning algorytmu Cheat arkusza** pomaga wybrać hello prawo algorytmu dla modelu analizy predykcyjnej.

[Azure Machine Learning Studio](https://studio.azureml.net/) ma dużej biblioteki algorytmów z hello ***regresji***, ***klasyfikacji***, ***klastrowanie***i ***wykrywania anomalii*** rodziny. Każdy jest zaprojektowana tooaddress innego typu machine learning problem.

## <a name="download-machine-learning-algorithm-cheat-sheet"></a>Pobieranie: Machine learning algorytmu ściągawka
**Pobierz hello ściągawka tutaj: [Learning Algorithm Cheat arkuszu maszyny (11 x 17 cali)](http://download.microsoft.com/download/A/6/1/A613E11E-8F9C-424A-B99D-65344785C288/microsoft-machine-learning-algorithm-cheat-sheet-v6.pdf)**

![Arkusz ze wskazówkami dotyczącymi Algorytm uczenia maszyny: Dowiedz się, jak toochoose Algorytm uczenia maszynowego.][cheat-sheet]

[cheat-sheet]: ./media/machine-learning-algorithm-cheat-sheet/machine-learning-algorithm-cheat-sheet-small_v_0_6-01.png

Pobrać i wydrukować hello maszyny Learning Algorithm Cheat arkusza w tookeep rozmiarze tabloidu go pod ręką i get ułatwić sobie wybór algorytmu.

> [!NOTE]
> Zobacz artykuł hello [jak toochoose algorytmów uczenia maszynowego Azure Microsoft](machine-learning-algorithm-choice.md) dla toousing szczegółowy przewodnik ten arkusz ze wskazówkami.
> 
> 

## <a name="more-help-with-algorithms"></a>Więcej informacji o algorytmy
* Aby uzyskać pomoc przy użyciu tego arkusza cheat dotyczące wybierania hello algorytm prawo, a także bardziej omówienie hello różne typy algorytmów uczenia maszynowego i sposób ich używania, zobacz [jak Microsoft Azure Machine Learningalgorytmówtoochoose](machine-learning-algorithm-choice.md).
* Aby infographic do pobrania, opisujący algorytmów i przykłady, zobacz [Infographic do pobrania: Machine learning podstawy wraz z przykładami algorytmu](machine-learning-basics-infographic-with-algorithm-examples.md).
* Aby uzyskać listę według kategorii wszystkich hello algorytmów uczenia maszynowego dostępnych w usłudze Machine Learning Studio, zobacz [zainicjować modelu] [ initialize-model] hello Machine Learning Studio algorytmu i pomóc w Module.
* Aby uzyskać alfabetyczną listę wszystkich algorytmów i modułów w usłudze Machine Learning Studio, zobacz [A — Z listy modułów usługi Machine Learning Studio] [ a-z-list] algorytmu Studio uczenia maszynowego i pomóc w Module.
* toodownload i Drukuj diagram, który zawiera omówienie funkcji hello usługi Machine Learning Studio, zobacz [diagram przeglądowy możliwości usługi Azure Machine Learning Studio](machine-learning-studio-overview-diagram.md).

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="notes-and-terminology-definitions-for-hello-machine-learning-algorithm-cheat-sheet"></a>Uwagi i definicje terminów dla Algorytm uczenia maszynowego hello ściągawka

* Sugestie Hello oferowana w tym arkuszu, wskazówkami algorytmu są przybliżonej reguły z podglądu. Niektóre mogą być wygięte, a niektóre mogą flagrantly naruszone. Jest to zamierzone toosuggest punkt początkowy. Nie można toorun obawiasz się head-to-head konkurencji między kilka algorytmów na podstawie danych. Nie jest po prostu nie zastąpi opis zasad hello poszczególnych algorytmów i opis hello systemu, które wygenerowało dane.

* Każdy algorytmu uczenia maszynowego ma własnego stylu lub *indukcyjna odchylenia*. Dla konkretnego problemu odpowiednie może być kilka algorytmów i jeden algorytm może być lepszym rozwiązaniem niż inne. Ale nie zawsze jest możliwe tooknow wcześniej co hello najlepsze dopasowanie. W takich przypadkach kilka algorytmy są wyświetlane razem w przydatną ściągawkę hello. Właściwej strategii będzie można tootry jeden algorytm, a jeśli wyniki hello nie są jeszcze zadowalające, spróbuj hello innych użytkowników. Oto przykład z hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com/) eksperymentu, która próbuje kilka algorytmów przed hello tych samych danych i porównuje hello wyniki: [porównania klasyfikatory wielu klas: list rozpoznawania ](http://gallery.cortanaintelligence.com/Details/a635502fc98b402a890efe21cec65b92).

* Istnieją trzy główne kategorie uczenia maszynowego: **uczenia nadzorowanego**, **uczenie nienadzorowane**, i **learning wzmocnienie**.

  * W **uczenia nadzorowanego**, etykietą lub skojarzone z kategorii lub wartości istotnej każdego punktu danych.  Przykład etykiety kategorii jest przypisywanie obrazu jako "kot" lub "dog".  Przykład etykiety wartość to cena sprzedaży hello skojarzone z używanego samochodu. Witaj celem uczenia nadzorowanego jest toostudy etykietą wiele przykłady takich, a następnie toobe toomake stanie prognoz dotyczących punktów danych w przyszłości. Na przykład identyfikowanie nowe fotografie za pomocą hello poprawne zwierzę lub przypisywanie tooother ceny sprzedaży dokładne używane samochodów. Jest to popularnych i przydatne typu uczenia maszynowego. Wszystkie moduły hello w usłudze Azure Machine Learning są uczenia nadzorowanego algorytmów z wyjątkiem [klastrowanie K-średnich][k-means-clustering].

  * W **uczenie nienadzorowane**, punkty danych mają bez etykiet skojarzonych z nimi. Zamiast tego hello celem Algorytm uczenia nienadzorowanych jest tooorganize hello danych w niektórych toodescribe lub sposób jego struktury. Oznacza to, grupowanie w klastrach, tak jak w przypadku K-średnich lub znajdowania różne sposoby patrzeć dane złożone, aby był wyświetlany prostsze.

  * W **learning wzmocnienie**, algorytm hello pobiera toochoose akcji w punkcie danych tooeach odpowiedzi. Jest typowym podejściem w robotics, gdzie hello zbiór odczyty czujników w jednym punkcie w czasie jest punkt danych, a algorytm hello należy wybrać robota hello następnej akcji. Istnieje również fizyczną nadające się do aplikacji Internetu rzeczy. Algorytm uczenia Hello również odbiera sygnał osób trzecich, to chwilę później, wskazującą, jaka hello decyzji. Oparte na to, algorytm hello modyfikuje jego strategii w kolejności tooachieve hello najwyższy osób trzecich. Obecnie nie ma żadnych wzmocnienie uczenia moduły Algorytm uczenia Maszynowego Azure.

* **Metody Estymacja Bayesian** upewnij założeń hello statystycznie niezależnych punktów danych. Oznacza to, że hello unmodeled zmienności jednego punktu danych jest nieskorelowane osobom, oznacza to, że nie można przewidzieć. Na przykład jeśli dane hello rejestrowane są hello liczbę minut, aż do następnego pociągu całość hello dociera dwóch pomiarów dziennie od siebie są statystycznie niezależne. Jednak dwóch pomiarów kilka minut od siebie nie są one statystycznie niezależne — hello wartość jednego jest wysoce predykcyjnej hello wartości hello innych.

* **Boosted regresji drzewa decyzyjnego** korzysta z funkcji nakładają się na siebie lub interakcji między funkcjami. Czy oznacza, że w danych danego punktu hello wartość jedną funkcję jest nieco predykcyjnej wartości hello innego typu. Na przykład w codziennych danych temperatury wysokiej/niskie, wiedzy o niskiej temperatury hello dzień hello pozwala toomake uzasadnione wynik na powitania wysoki. Hello informacje zawarte w dwie funkcje hello jest nieco nadmiarowy.

* Klasyfikacji danych na więcej niż dwie kategorie może odbywać się przy użyciu klasyfikatora z założenia wielu klas, lub łącząc zestaw klasyfikatory dwuklasowych do **zespół**. W podejściu zespół hello, jest oddzielny klasyfikatora dwuklasowych dla każdej klasy — każdy z nich oddziela danych hello na dwie kategorie: "tej klasy" i "nie tej klasy." Następnie te klasyfikatory głosowania hello przydziału poprawne hello punktu danych. Jest zasada operacyjne hello za [Multiklasa jedna kontra wszystkie][one-vs-all-multiclass].

* Załóżmy kilka metod, w tym Regresja logistyczna i maszyna punktu Bayesa hello, **granice liniowej klasy**. Oznacza to, ich założono, że hello granice między klasami są około proste (lub hyperplanes w hello bardziej ogólne przypadku). Często jest to cecha hello danych czy nie znasz dopiero po podjęto tooseparate go, ale jest to zwykle mogą być rozpoznawane przez wizualizacja wcześniej. Jeżeli granice klasy hello wygląda bardzo nieregularne, przestrzegaj drzew decyzyjnych, decyzja dżungle, obsługuje wektor maszyny lub sieci neuronowej.

* Sieci neuronowe mogą być używane z kategorii zmiennymi przez tworzenie **fikcyjny zmiennej** dla każdej kategorii ustawieniem dla niego too1 w przypadkach, gdy hello kategoria ma zastosowanie, 0, w którym nie.


<!-- This is how you can embed a link in an image in HTML. Don't know how toodo this in markdown.
<a href="http://download.microsoft.com/download/A/6/1/A613E11E-8F9C-424A-B99D-65344785C288/microsoft-machine-learning-algorithm-cheat-sheet.pdf">
<img src="C:\Users\garye\azure-docs-pr\articles\media\machine-learning-algorithm-cheat-sheet\cheat-sheet-small.png">
</a>
-->

<!-- Module References -->
[a-z-list]: https://msdn.microsoft.com/library/azure/dn906033.aspx
[initialize-model]: https://msdn.microsoft.com/library/azure/0c67013c-bfbc-428b-87f3-f552d8dd41f6/
[k-means-clustering]: https://msdn.microsoft.com/library/azure/5049a09b-bd90-4c4e-9b46-7c87e3a36810/
[one-vs-all-multiclass]: https://msdn.microsoft.com/library/azure/7191efae-b4b1-4d03-a6f8-7205f87be664/
