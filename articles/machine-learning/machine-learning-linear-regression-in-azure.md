---
title: aaaUsing regresji liniowej w uczeniu maszynowym | Dokumentacja firmy Microsoft
description: "Porównanie modeli regresji liniowej w programie Excel, jak i w usłudze Azure Machine Learning Studio"
metakeywords: 
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 417ae6ab-de4f-4bdd-957a-d96133234656
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: kbaroni;garye
ms.openlocfilehash: 8716040ad296053a72fb06c7c9660a186123ac15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-linear-regression-in-azure-machine-learning"></a>Używanie regresji liniowej w usłudze Azure Machine Learning
> *Kate Baroni* i *Ben Boatman* są architekci rozwiązań w firmy Microsoft danych usługi Insights centrum doskonałości przedsiębiorstwa. W tym artykule opisano w nich ich obsługi migrowania istniejących regresji analizy suite tooa rozwiązania w chmurze przy użyciu usługi Azure Machine Learning. 
> 
> 

&nbsp; 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="goal"></a>Cel
Nasze projektu wprowadzenie do dwóch celów pamiętać: 

1. Użyj analizy predykcyjnej tooimprove hello dokładność naszej organizacji miesięczne projekcje przychodu 
2. Użyj usługi Azure Machine Learning tooconfirm, optymalizacja, zwiększyć szybkość pracy i skali naszych wyników. 

Jak wiele firm naszej organizacji przechodzi przez miesięczne przychodów, funkcja prognozowania procesu. Mały zespół analitycy biznesowi został zlecił mu za pomocą usługi Azure Machine Learning toosupport hello procesu i zwiększenia dokładności prognozy. zespół Hello przeznaczonego kilka miesięcy zbieranie danych z wielu źródeł i uruchamianie hello atrybuty danych za pomocą analizy statystycznej identyfikowanie prognozowania sprzedaży tooservices odpowiednich atrybutów klucza. następnym krokiem Hello został toobegin prototypowania statystyczne regresji modeli na powitania danych w programie Excel. W ciągu kilku tygodni było Excel model regresji, który został outperforming hello bieżącego pola i finance procesy prognozowania. To stała się hello linii bazowej przewidywania wyników. 

Następnie Wybraliśmy hello następny krok toomoving naszych analizy predykcyjnej za pośrednictwem toofind uczenia maszynowego tooAzure się, jak uczenia maszynowego można ulepszyć na wydajność predykcyjnej.

## <a name="achieving-predictive-performance-parity"></a>Obsługiwanie parzystości predykcyjnej wydajności
Nasze priorytet został parzystości tooachieve między modelami regresji uczenia maszynowego i Excel. Podane hello tych samych danych i hello sam podziału dla celów szkoleniowych i testów danych, możemy parzystości predykcyjnej wydajności tooachieve pomiędzy programami Excel i uczenia maszynowego. Początkowo firma Microsoft nie powiodło się. model programu Excel Hello outperformed hello modelu uczenia maszynowego. Błąd Hello: ze względu na brak tooa zrozumienie podstawowego narzędzia hello ustawienie w uczeniu maszynowym. Po zakończeniu synchronizacji z zespół pracujący nad produktem hello uczenia maszynowego firma Microsoft zdobytych lepiej zrozumieć hello podstawowe ustawienia wymagane dla naszych zestawów danych i osiągnięte parzystości między dwa modele hello. 

### <a name="create-regression-model-in-excel"></a>Utwórz model regresji w programie Excel
Nasze regresji Excel używane hello standardowe regresji liniowej modelu znaleziono w hello ToolPak analizy programu Excel. 

Firma Microsoft obliczana *średniej % bezwzględny błąd* i używać go jako miara wydajności hello hello modelu. Zajęło tooarrive 3 miesiące w modelu pracy przy użyciu programu Excel. Firma Microsoft wprowadzane większość uczenia hello na powitania eksperymentu Machine Learning Studio, co ostatecznie było korzystne w opis wymagań.

### <a name="create-comparable-experiment-in-azure-machine-learning"></a>Tworzenie porównywalnych eksperymentu w usłudze Azure Machine Learning
Te kroki toocreate była naszych eksperymentu w usłudze Machine Learning Studio: 

1. Zestaw danych hello przekazane jako tooMachine pliku csv Learning Studio (bardzo mały plik)
2. Utworzony nowy eksperyment i hello [Select Columns in Dataset] [ select-columns] tooselect modułu hello te same funkcje danych używany w programie Excel 
3. Używane hello [podziału danych] [ split] modułu (z *wyrażenia względne* tryb) toodivide hello danych do tego samego szkolenia zestawów danych Witaj, podobnie jak w programie Excel 
4. Badawcze, mające z hello [regresji liniowej] [ linear-regression] modułu (tylko opcje domyślne), udokumentowane i porównać modelu regresji hello wyniki tooour programu Excel

### <a name="review-initial-results"></a>Przejrzyj wyniki początkowej
Na początku modelu programu Excel hello wyraźnie outperformed hello modelu usługi Machine Learning Studio: 

|  | Excel | Studio |
| --- |:---:|:---:|
| Wydajność | | |
| <ul style="list-style-type: none;"><li>Dostosowana R-kwadrat</li></ul> |0.96 |Nie dotyczy |
| <ul style="list-style-type: none;"><li>Współczynnik <br />Oznaczanie</li></ul> |Nie dotyczy |0.78<br />(dokładność niski) |
| Oznacza błąd absolutny |$9. 5M |$ 19.4 M |
| Oznacza błąd absolutny (%) |6.03% |12.2% |

Wystąpił naszych procesu i wyniki przez hello programistów i analityków danych na powitania zespół usługi Machine Learning, one szybko udostępniane niektóre przydatne porady. 

* Jeśli używasz hello [regresji liniowej] [ linear-regression] modułu w usłudze Machine Learning Studio, znajdują się dwie metody:
  * Spadku gradientu online: Bardziej odpowiednie dla dużą skalę problemów może być
  * Zwykłe najmniejszych kwadratów: To metoda hello większość osób postrzega podczas ich usłyszeć regresji liniowej. W przypadku małych zestawów danych zwykłej najmniejszych kwadratów może być bardziej optymalnym wyborem.
* Należy rozważyć Dostosowywanie hello wagi uregulowania L2 parametru tooimprove wydajności. Too0.001 jest ustawiona domyślnie, ale dla naszych niewielki zestaw danych możemy ustawić too0.005 tooimprove wydajności. 

### <a name="mystery-solved"></a>Taki rozwiązanie!
Stosowania zaleceń hello, firma Microsoft uzyskuje hello tej samej linii bazowej wydajności w usłudze Machine Learning Studio, podobnie jak w przypadku programu Excel: 

|  | Excel | Studio (początkowego) | Studio z najmniejszych kwadratów |
| --- |:---:|:---:|:---:|
| Wartość etykietą |Rzeczywiste (numeryczne) |tym samym |tym samym |
| Uczeń |Excel -> dane analizy -> regresji |Regresji liniowej. |Regresja liniowa |
| Opcje uczeń |Nie dotyczy |Wartości domyślne |zwykłe najmniejszych kwadratów<br />L2 = 0,005 |
| Zestaw danych |26 wierszy, funkcje 3, 1 etykiety. Wszystkie liczbowe. |tym samym |tym samym |
| Podziel: pociągu |Excel ćwiczenie hello najpierw 18 wierszy, przetestowane na powitania ostatnie 8 wierszy. |tym samym |tym samym |
| Podziel: testu |Formuła regresji zastosowane w programie Excel toohello ostatnie wiersze 8 |tym samym |tym samym |
| **Wydajność** | | | |
| Dostosowana R-kwadrat |0.96 |Nie dotyczy | |
| Współczynnik determinacji |Nie dotyczy |0.78 |0.952049 |
| Oznacza błąd absolutny |$9. 5M |$ 19.4 M |$9. 5M |
| Oznacza błąd absolutny (%) |<span style="background-color: 00FF00;"> 6.03%</span> |12.2% |<span style="background-color: 00FF00;"> 6.03%</span> |

Ponadto dobrze toohello funkcji obciążenia w hello Azure uczonego modelu porównaniu hello współczynników programu Excel:

|  | Współczynniki programu Excel | Wagi funkcji platformy Azure |
| --- |:---:|:---:|
| ODCIĘTA/odchylenia |19470209.88 |19328500 |
| Funkcja A programu |0.832653063 |0.834156 |
| Funkcja B |11071967.08 |11007300 |
| Funkcja C |25383318.09 |25140800 |

## <a name="next-steps"></a>Następne kroki
Możemy usługi sieci web uczenie maszynowe hello tooconsume programu Excel. Nasze analitycy biznesowi rozwiązania korzystają z programu Excel i firma Microsoft potrzebne hello toocall sposób Machine Learning web service z wierszem danych programu Microsoft Excel i jest zwracany hello przewidzieć tooExcel wartość. 

Ponadto możemy toooptimize naszego modelu przy użyciu opcji hello i algorytmy dostępne w usłudze Machine Learning Studio.

### <a name="integration-with-excel"></a>Integracja z programem Excel
Nasze rozwiązanie zostało toooperationalize naszych regresji Machine Learning model przez utworzenie usługi sieci web z hello trenowanego modelu. W ciągu kilku minut hello Usługa sieci web została utworzona i może nazywamy go bezpośrednio z programu Excel tooreturn wartość przychodu przewidywane. 

Witaj *pulpitu nawigacyjnego usług sieci Web* znajdują się w skoroszycie programu Excel do pobrania. skoroszyt Hello zawiera wstępnie sformatowane hello informacji usługi sieci web interfejsu API i schematów osadzonych. Po kliknięciu *Pobierz skoroszyt programu Excel*, zostanie otwarty skoroszyt hello i można go zapisać tooyour komputera lokalnego. 

![][1]

Otwórz skoroszycie hello skopiuj wstępnie zdefiniowane parametry do sekcji parametr hello niebieski, jak pokazano poniżej. Po wpisaniu są parametry hello, Excel uwidacznia toohello usługi sieci web uczenie maszynowe i hello przewidywane etykiety scored będą wyświetlane w sekcji przewidywane wartości hello zielony. skoroszyt Hello będzie toocreate prognoz dla parametrów, na podstawie uczonego modelu dla wszystkich elementów wiersza objęte parametrów. Aby uzyskać więcej informacji dotyczących sposobu toouse tej funkcji, zobacz [konsumowania usługi sieci Web Azure Machine Learning z programu Excel](machine-learning-consuming-from-excel.md). 

![][2]

### <a name="optimization-and-further-experiments"></a>Optymalizacja i dalszych eksperymentów.
Teraz, gdy było linii bazowej z modelu programu Excel, przenieśliśmy wyprzedzeniem toooptimize naszych modelu uczenia maszynowego liniowej regresji. Użyliśmy modułu hello [na podstawie filtru wybór funkcji] [ filter-based-feature-selection] tooimprove na naszych zaznaczenia elementów początkowych danych oraz jej pomogły osiągnąć lepszą wydajność, 4.6% oznacza błąd absolutny. Dla przyszłych projektów użyjemy tej funkcji, który może zapisać nam tygodnie w iteracji danych atrybutów toofind hello prawidłowego zestawu funkcji toouse modelowania. 

Następnie planujemy tooinclude dodatkowych algorytmów, takich jak [Estymacja Bayesian] [ bayesian-linear-regression] lub [Boosted drzew decyzyjnych] [ boosted-decision-tree-regression] w naszym toocompare eksperymentu wydajność. 

Jeśli chcesz tooexperiment z regresji, tootry dobrej zestawu danych jest hello regresji wydajności energii przykładowego zestawu danych, który ma wiele atrybutów wartości liczbowych. zestaw danych Hello jest dostarczane jako część hello przykładowych zestawów danych w usłudze Machine Learning Studio. Można skorzystać z szeregu toopredict modułów uczenia ogrzewania obciążenia lub chłodzenia obciążenia. Wykres Hello poniżej znajduje się porównanie wydajności różnych regresji uzyskuje informacje o przed przewidywania dataset zapotrzebowania na energię hello, dla hello docelowy zmiennej chłodzenia obciążenia: 

| Model | Oznacza błąd absolutny | Błąd kwadrat średniej głównego | Względny błąd absolutny | Względna kwadrat błąd | Współczynnik determinacji |
| --- | --- | --- | --- | --- | --- |
| Drzewo decyzyjne boosted |0.930113 |1.4239 |0.106647 |0.021662 |0.978338 |
| Regresja liniowa (spadku gradientu) |2.035693 |2.98006 |0.233414 |0.094881 |0.905119 |
| Regresja sieci neuronowej |1.548195 |2.114617 |0.177517 |0.047774 |0.952226 |
| Regresja liniowa (zwykłej najmniejszych kwadratów) |1.428273 |1.984461 |0.163767 |0.042074 |0.957926 |

## <a name="key-takeaways"></a>Takeaways klucza
Dowiedzieliśmy się znacznie przez z uruchomionych regresji programu Excel i usługi Azure Machine Learning experiments równolegle. Tworzenie modelu linii bazowej hello w programie Excel i należy go porównać toomodels za pomocą uczenia maszynowego [regresji liniowej] [ linear-regression] pomógł nam informacje uczenie maszynowe Azure i firma Microsoft odnalezionych danych tooimprove możliwości Wybór i modelu wydajności. 

Również znaleźć jest wskazane toouse [na podstawie filtru wybór funkcji] [ filter-based-feature-selection] tooaccelerate przewidywania przyszłych projektów. Stosując funkcję wyboru tooyour danych, można utworzyć model ulepszone w uczeniu maszynowym z lepszą ogólną wydajność. 

Witaj możliwości tootransfer Witaj predykcyjnej analityczne prognozowania z uczenia maszynowego tooExcel systemically umożliwia znaczne zwiększenie toosuccessfully możliwości hello udostępniania wyników tooa szerokie biznesowych użytkownika odbiorców. 

## <a name="resources"></a>Zasoby
Poniżej przedstawiono niektóre zasoby pomagające w pracy z regresji: 

* Regresja w programie Excel. Jeśli nigdy nie podjęto regresji w programie Excel, w tym samouczku ułatwia: [http://www.excel-easy.com/examples/regression.html](http://www.excel-easy.com/examples/regression.html)
* Funkcja prognozowania vs regresji. Tyler Chessman zapisano artykułu blog, wyjaśniający, jak toodo czasu serii prognozowania w programie Excel, zawiera opis dla początkujących dobrej regresji liniowej. [http://sqlmag.com/SQL-Server-Analysis-Services/Understanding-Time-Series-forecasting-Concepts](http://sqlmag.com/sql-server-analysis-services/understanding-time-series-forecasting-concepts) 
* Regresja liniowa zwykłej najmniejszych kwadratów: Wady, problemów i problemów. Wprowadzenie oraz omówienie regresji: [http://www.clockbackward.com/2009/06/18/ordinary-least-squares-linear-regression-flaws-problems-and-pitfalls/](http://www.clockbackward.com/2009/06/18/ordinary-least-squares-linear-regression-flaws-problems-and-pitfalls/)

[1]: ./media/machine-learning-linear-regression-in-azure/machine-learning-linear-regression-in-azure-1.png
[2]: ./media/machine-learning-linear-regression-in-azure/machine-learning-linear-regression-in-azure-2.png


<!-- Module References -->
[bayesian-linear-regression]: https://msdn.microsoft.com/library/azure/ee12de50-2b34-4145-aec0-23e0485da308/
[boosted-decision-tree-regression]: https://msdn.microsoft.com/library/azure/0207d252-6c41-4c77-84c3-73bdf1ac5960/
[filter-based-feature-selection]: https://msdn.microsoft.com/library/azure/918b356b-045c-412b-aa12-94a1d2dad90f/
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/

