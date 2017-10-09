---
title: aaaExecute Python machine learning skrypty | Dokumentacja firmy Microsoft
description: "Przedstawiono projektowania zasad podstawowej obsługi skryptów języka Python w usłudze Azure Machine Learning i scenariusze użycia podstawowe, możliwości i ograniczeń."
keywords: "Python uczenia maszynowego, pandas, pandas języka python, skrypty języka python, wykonywanie skryptów języka python"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: ee9eb764-0d3e-4104-a797-19fc29345d39
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: bradsev
ms.openlocfilehash: 8d23aaa972a46cb1a07ea0f18cc1e24933fe3e6f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="execute-python-machine-learning-scripts-in-azure-machine-learning-studio"></a>Wykonywanie skryptów uczenia maszynowego w języku Python w usłudze Azure Machine Learning Studio

W tym temacie opisano zasady projektowania hello bazowy hello bieżącej obsługi skryptów języka Python w usłudze Azure Machine Learning. Witaj głównego możliwości opisano również, w tym:

- wykonanie scenariusze użycia podstawowe
- wynik eksperymentu w usłudze sieci web
- Obsługa importowania istniejącego kodu
- Eksportuj wizualizacji
- Wykonaj nadzorowane funkcji wyboru
- zrozumieć następujące ograniczenia

[Python](https://www.python.org/) jest narzędziem niezbędne w piersi narzędzia hello z wielu analityków danych. Posiada:

* Składnia elegancki i zwięzłe 
* Obsługa platform 
* zbiór przeważająca zaawansowanych bibliotek i 
* Narzędzia deweloperskie dojrzała. 

Python jest używany we wszystkich fazach zwykle używanych w machine learning modelowania przepływu pracy:

- pozyskiwania danych i przetwarzania 
- Funkcja konstrukcji
- szkolenie modelu 
- Weryfikacja modelu
- Wdrażanie modeli hello

Azure Machine Learning Studio obsługuje osadzania skrypty języka Python do różnych części maszyny eksperymentu uczenia, a także bezproblemowo opublikować go jako usługi sieci web w systemie Microsoft Azure.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]


## <a name="design-principles-of-python-scripts-in-machine-learning"></a>Projektowanie zasad skrypty języka Python w uczeniu maszynowym

tooPython podstawowy interfejs Hello w usłudze Azure Machine Learning Studio odbywa się za pośrednictwem hello [wykonanie skryptu Python] [ execute-python-script] modułu pokazany na rysunku 1.

![image1](./media/machine-learning-execute-python-scripts/execute-machine-learning-python-scripts-module.png)

![image2](./media/machine-learning-execute-python-scripts/embedded-machine-learning-python-script.png)

Rysunek 1. Witaj **wykonanie skryptu Python** modułu.

Witaj [wykonanie skryptu Python] [ execute-python-script] modułu w usłudze Azure ML Studio akceptuje się dane wejściowe toothree i tworzy się dane wyjściowe tootwo (szczegółowo opisane w następujących sekcji hello), takie jak jego analogowy R hello [ Wykonanie skryptu języka R] [ execute-r-script] modułu. Witaj toobe kodu Python wykonywane jest wprowadzany do hello parametrów jako specjalnie nazwanego punktu wejścia funkcji o nazwie `azureml_main`. Poniżej przedstawiono hello klucza projektowy zasady używane tooimplement ten moduł:

1. *Musi być idiomatyczne dla użytkowników języka Python.* Większość użytkowników Python współczynnika ich kodu jako funkcje w modułach. Dlatego przełączenie dużo wykonywanych instrukcji w module najwyższego poziomu jest stosunkowo rzadkie. W związku z tym pole skryptu hello również przyjmuje specjalnej funkcji Python jako min. toojust sekwencji instrukcji. Witaj obiekty widoczne w funkcji hello są standardowe typy biblioteka języka Python takich jak [Pandas](http://pandas.pydata.org/) ramek danych i [NumPy](http://www.numpy.org/) tablic.
2. *Musi mieć o wysokiej wierności między lokalnym i w chmurze wykonania.* Witaj hello tooexecute wewnętrznej bazy danych używane kodu Python opiera się na [Anaconda](https://store.continuum.io/cshop/anaconda/), powszechnie używane i platform naukowych dystrybucję oprogramowania Python. Dołączono Zamknij too200 hello najbardziej typowych pakietów języka Python. W związku z tym analityków danych może debugowania i kwalifikuj ich kodu w środowisku Azure Machine Learning zgodnego Anaconda lokalnego. Następnie użyj istniejącego środowiska programowania, takiego jak [IPython](http://ipython.org/) notesu lub [narzędzi Python Tools for Visual Studio](http://aka.ms/ptvs), toorun w ramach eksperymentu uczenia Maszynowego Azure. Witaj `azureml_main` punktu wejścia jest podstawowego funkcja Python i dlatego *** można tworzyć bez usługi Azure ML unikatowy kod lub hello zainstalowany zestaw SDK.
3. *Musi być bezproblemowe zezwala na składanie z innych modułów uczenia maszynowego Azure.* Witaj [wykonanie skryptu Python] [ execute-python-script] modułu akceptuje jako wejściach i wyjściach, standardowe zestawy danych usługi Azure Machine Learning. Witaj podstawowej struktury przezroczyste i wydajne pomost hello środowisk uruchomieniowych uczenie Maszynowe Azure i Python. Python można więc w połączeniu z istniejących uczenie Maszynowe Azure przepływów pracy, włącznie z tymi, które wywołują R i SQLite. Wynik, naukowca danych tworzą przepływy pracy który:
   * Użyj Python i Pandas danych, przetwarzanie wstępne i czyszczenia
   * hello źródła danych tooa SQL przekształcania, dołączenie wiele funkcji tooform zbiory danych
   * modele Train przy użyciu hello algorytmy w usłudze Azure Machine Learning 
   * Oceń i po przetwarzaniu hello wyników za pomocą R.


## <a name="basic-usage-scenarios-in-ml-for-python-scripts"></a>Scenariusze użycia podstawowe w ML skrypty języka Python

W tej sekcji możemy badania niektórych podstawowych zastosowań hello hello [wykonanie skryptu Python] [ execute-python-script] modułu. Moduł Python toohello dane wejściowe są widoczne jako Pandas ramek danych. Witaj funkcja musi zwracać jedną ramkę danych Pandas umieszczone wewnątrz Python [sekwencji](https://docs.python.org/2/c-api/sequence.html) przykład spójnej kolekcji, listy lub tablicy NumPy. pierwszy element Hello tej sekwencji jest następnie zwracany w hello pierwszy port wyjściowy modułu hello. Ten schemat jest pokazany na rysunku 2.

![image3](./media/machine-learning-execute-python-scripts/map-of-python-script-inputs-outputs.png)

Rysunek 2. Mapowanie tooparameters porty wejściowe i zwrócić wartość portu toooutput.

Bardziej szczegółowe semantykę jak porty wejściowe hello uzyskać zamapowanej tooparameters z hello `azureml_main` funkcji są wyświetlane w tabeli 1:

![image1T](./media/machine-learning-execute-python-scripts/python-script-inputs-mapped-to-parameters.png)

Tabela 1. Mapowanie parametrów toofunction portów wejściowych.

Witaj mapowanie między porty wejściowe i parametry funkcji jest pozycyjnych:

- Hello pierwszy port wejściowy połączonych jest pierwszy parametr funkcji hello toohello mapowane. 
- Hello drugiej danej wejściowej (jeśli jest podłączony) jest drugi parametr funkcji hello toohello mapowane.

Zobacz *Python do analizy danych* (O'Reilly 2012) przez McKinney Zach. Aby uzyskać więcej informacji na Python Pandas i jak efektywne może być toomanipulate używanych danych. 


## <a name="translation-of-input-and-output-types"></a>Tłumaczenie typy wejściowe i wyjściowe 
Wejściowe zestawy danych w uczenie Maszynowe Azure są ramki przekonwertowanego toodata w Pandas. Ramek danych wyjściowych dokonywana jest konwersja wstecz tooAzure ML zestawów danych. wykonywane są następujące konwersje Hello:

1. Ciąg, jak i numeryczne kolumn są konwertowane na — jest i brakujące wartości w zestawie danych są przekonwertowanego too'NA "wartości Pandas. Hello tego samego Konwersja odbywa się w sposób ponownie hello (wartości NA Pandas są wartości przekonwertowane toomissing uczenie Maszynowe Azure).
2. Wektory indeksu w Pandas nie są obsługiwane w uczenie Maszynowe Azure. Wszystkie ramki danych wejściowych w funkcji Python hello zawsze ma 64-bitowych indeksu numerycznych od 0 toohello liczby wierszy pomniejszonej o 1. 
3. Azure ML zestawy danych nie może zawierać zduplikowanych nazw kolumn i nazwy kolumn, które nie są ciągami. Jeśli ramki danych wyjściowych zawiera nieliczbowy kolumn, hello wywołania framework `str` na powitania nazw kolumn. Podobnie, zduplikowanych nazw kolumn są automatycznie zniekształcone tooinsure hello nazwy są unikatowe. sufiks Hello (2) zostanie dodany toohello duplikat pierwszy, drugi duplikat toohello (3) i tak dalej.


## <a name="operationalizing-python-scripts"></a>Operacyjnych skrypty języka Python

Wszelkie [wykonanie skryptu Python] [ execute-python-script] moduły używane w eksperymencie oceniania są wywoływane, gdy publikowane jako usługi sieci web. Przykładowo rysunek 3 przedstawia oceniania eksperymentu, która zawiera tooevaluate kodu hello pojedyncze wyrażenie języka Python. 

![image4](./media/machine-learning-execute-python-scripts/figure3a.png)

![image5](./media/machine-learning-execute-python-scripts/python-script-with-python-pandas.png)

Rysunek 3. Usługa sieci Web do obliczenia wyrażenia języka Python.

Utworzone na podstawie tego eksperymentu usługi sieci web:

- przyjmuje jako dane wejściowe wyrażenia języka Python (jako ciąg)
- wysyła on toohello interpreter języka Python 
- zwraca tabelę zawierającą zarówno wyrażenie hello i wynik hello obliczone.


## <a name="importing-existing-python-script-modules"></a>Importowanie istniejących moduły skryptu języka Python

Typowe przypadek użycia dla wielu analityków danych jest tooincorporate istniejące skrypty języka Python do eksperymentów uczenie Maszynowe Azure. Zamiast konieczności czy cały kod jest połączonych i wkleić w polu jednego skryptu, hello [wykonanie skryptu Python] [ execute-python-script] modułu akceptuje plik zip, który zawiera moduły Python hello trzeci portu wejściowego. rozpakowane jest plik Hello przez platformę wykonywania hello w czasie wykonywania i hello zawartości są dodawane ścieżki biblioteki toohello hello interpreter języka Python. Witaj `azureml_main` punktu wejścia funkcji można następnie zaimportować te moduły bezpośrednio.

Na przykład należy wziąć pod uwagę pliku hello Hello.py zawierający funkcję prosty "tekst Hello, World".

![image6](./media/machine-learning-execute-python-scripts/figure4.png)

Rysunek 4. Funkcja zdefiniowana przez użytkownika w pliku Hello.py.

Następnie utwórz plik Hello.zip, który zawiera Hello.py:

![image7](./media/machine-learning-execute-python-scripts/figure5.png)

Rysunek 5. Plik zip zawierający zdefiniowane przez użytkownika kod języka Python.

Przekaż plik zip hello jako zestawu danych w usłudze Azure Machine Learning Studio. Utwórz i uruchom eksperymentu, która używa hello Python kodu w pliku Hello.zip hello dołączając toohello trzeci port wejściowy z hello **wykonanie skryptu Python** modułu, jak pokazano na poniższym rysunku.

![image8](./media/machine-learning-execute-python-scripts/figure6a.png)

![image9](./media/machine-learning-execute-python-scripts/figure6b.png)

Rysunek 6. Przekazano eksperymentu przykładowego kodu Python zdefiniowane przez użytkownika jako plik zip.

danych wyjściowych modułu Hello pokazuje, że plik zip hello został rozpakowanych i że działają hello `print_hello` zostało uruchomione.
 
![image10](./media/machine-learning-execute-python-scripts/figure7.png)

Rysunek 7. Zdefiniowane przez użytkownika funkcja używana wewnątrz hello [wykonanie skryptu Python] [ execute-python-script] modułu.


## <a name="working-with-visualizations"></a>Praca z wizualizacji

Wykresy utworzone za pomocą MatplotLib, który można wywołać w przeglądarce hello może być zwracany przez hello [wykonanie skryptu Python][execute-python-script]. Ale hello powierzchnie nie są automatycznie przekierowane tooimages są one przy użyciu R. Dzięki użytkownika hello jawnie zapisać wszelkie powierzchni tooPNG plików, jeśli są one toobe zwrócił wstecz tooAzure uczenia maszynowego. 

toogenerate obrazów z MatplotLib, należy wykonać następujące procedury hello:

* Przełącz hello zaplecza za "AGG" z hello domyślne na podstawie Qt renderowania 
* Utwórz nowy obiekt rysunek 
* Pobierz hello osi i generowanie wszystkich powierzchni do niego 
* Zapisz plik PNG tooa rysunek hello 

Ten proces przedstawiono na powitania po rysunku 8, która tworzy wykres punktowy macierzy przy użyciu funkcji scatter_matrix hello w Pandas.

![image1v](./media/machine-learning-execute-python-scripts/figure-v1-8.png)

Rysunek 8. Kod toosave, który MatplotLib danych liczbowych tooimages.

Na rysunku nr 9 przedstawiono eksperymentu, która używa skryptu hello wcześniej przedstawić tooreturn geograficzne za pośrednictwem hello drugi port wyjściowy.

![image2v](./media/machine-learning-execute-python-scripts/figure-v2-9a.png) 

![image2v](./media/machine-learning-execute-python-scripts/figure-v2-9b.png) 

Rysunek 9. Wizualizacja powierzchni wygenerowane z kodu języka Python.

Jest możliwe tooreturn wiele wartości zapisując je w różnych obrazów, hello Azure Machine Learning środowiska uruchomieniowego przejmuje wszystkie obrazy i łączy je dla wizualizacji.


## <a name="advanced-examples"></a>Przykłady zaawansowane

środowisko Anaconda Hello zainstalowane w usłudze Azure Machine Learning zawiera pakiety wspólne, takie jak NumPy, SciPy i Scikits Dowiedz się więcej. Te pakiety można skutecznie dla różnych zadań przetwarzania danych w potoku uczenia maszynowego. Na przykład hello następujące eksperymentu i skryptu przedstawiają hello stosowania uczących zespół w Dowiedz się Scikits toocompute funkcji znaczenie wyniki dla zestawu danych. Hello wyniki mogą być używane tooperform nadzorowane wybór funkcji przed podawana do innego modelu uczenia Maszynowego.

Poniżej przedstawiono hello Python używana funkcja toocompute hello znaczenie wyniki i kolejność hello funkcji opartych na powitania wyników:

![image11](./media/machine-learning-execute-python-scripts/figure8.png)

Rysunek 10. Funkcja funkcje toorank przez wyniki.
 Witaj następujące eksperymentu następnie oblicza i zwraca wyniki znaczenie hello funkcji w zestawie danych "Pima indyjskiego cukrzyca" Witaj w usłudze Azure Machine Learning:

![image12](./media/machine-learning-execute-python-scripts/figure9a.png)
![image13](./media/machine-learning-execute-python-scripts/figure9b.png)    

Rysunek 11. Funkcje toorank eksperymentu w zestawie danych cukrzyca indyjskiego Pima hello.

## <a name="limitations"></a>Ograniczenia
Witaj [wykonanie skryptu Python] [ execute-python-script] ma obecnie hello następujące ograniczenia:

1. *Wykonywanie w trybie piaskownicy.* środowisko uruchomieniowe języka Python Hello jest obecnie w trybie piaskownicy i w związku z tym nie zezwala na dostęp do toohello sieci lub toohello lokalnego systemu plików w sposób ciągły. Wszystkie pliki zapisywane lokalnie są izolowane i usuwane po zakończeniu hello modułu. Hello kodu Python nie ma dostępu do większości katalogi na komputerze hello, w którym jest uruchamiany na, trwa wyjątek hello hello w bieżącym katalogu i jego podkatalogach.
2. *Brak zaawansowane programowanie i debugowanie pomocy technicznej.* Moduł Python Hello nie obsługuje obecnie IDE funkcje, takie jak intellisense i debugowanie. Ponadto jeśli moduł hello zakończy się niepowodzeniem w czasie wykonywania, hello pełne ślad stosu Python jest dostępna. Ale musi być wyświetlana w dzienniku danych wyjściowych hello hello modułu. Firma Microsoft zaleca obecnie opracowywania i debugowania skryptów języka Python w środowisku, na przykład IPython a następnie zaimportuj kod hello do hello modułu.
3. *Dane wyjściowe ramki danych.* punkt wejścia Python Hello jest tylko dozwolonych tooreturn ramki danych jako dane wyjściowe. Nie jest obecnie możliwe tooreturn, który dowolnego języka Python obiekty, takie jak modele przeszkolone kopii bezpośrednio toohello uczenie maszynowe Azure w czasie wykonywania. Podobnie jak [wykonanie skryptu języka R][execute-r-script], mającego hello samym ograniczeniom jest możliwe w wielu przypadkach obiekty toopickle na bajt tablicy, a następnie wróć który wewnątrz ramki danych.
4. *Brak możliwości toocustomize instalacji języka Python*. Witaj tylko sposób tooadd niestandardowych modułów środowiska Python jest obecnie za pomocą mechanizmu pliku zip hello opisany wcześniej. Gdy jest to możliwe w dla małych modułów, jest skomplikowane dla dużych modułów, (zwłaszcza z natywnych bibliotek DLL) lub dużej liczby modułów. 

## <a name="conclusions"></a>Wnioski
Witaj [wykonanie skryptu Python] [ execute-python-script] moduł pozwala naukowca danych tooincorporate istniejący kod języka Python do przepływów pracy learning maszyny hostowanych w chmurze w usłudze Azure Machine Learning i tooseamlessly operacjonalizuj je jako część usługi sieci web. Moduł skryptu Python Hello naturalnie współdziała z innych modułów w usłudze Azure Machine Learning. Moduł Hello może służyć szereg zadań przetwarzania toopre Eksploracja danych i wyodrębniania funkcji, a następnie tooevaluation i przetwarzania końcowego hello wyników. Witaj runtime wewnętrznej bazy danych używane do wykonywania jest oparta na platformę Anaconda — dystrybucję oprogramowania Python dobrze przetestowane i powszechnie używane. Ta zaplecza upraszcza dla Ciebie tablicy tooon istniejących zasobów kodu w chmurze hello.

Oczekujemy toohello dodatkowe funkcje tooprovide [wykonanie skryptu Python] [ execute-python-script] modułu, takich jak hello tootrain możliwości i operacjonalizuj modele w języku Python i tooadd lepszą obsługę hello Programowanie i debugowanie kodu w usłudze Azure Machine Learning Studio.

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji, zobacz hello [Centrum deweloperów języka Python](https://azure.microsoft.com/develop/python/).

<!-- Module References -->
[execute-python-script]: https://msdn.microsoft.com/library/azure/cdb56f95-7f4c-404d-bde7-5bb972e6f232/
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
